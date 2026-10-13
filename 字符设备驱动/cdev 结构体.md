用cdev 结构体描述一个字符设备，就像是注册一个字符设备，我们需要规定字符设备对应内核的设备号，与operasion结构体进行绑定。
#include <linux/module.h>

#include <linux/kernel.h>

#include <linux/init.h>

#include <linux/fs.h>

#include <linux/cdev.h>

  

// 1. 全局变量

dev_t dev_num;                // 存放设备号

struct cdev cdev_test;        // 字符设备结构体

  

// 2. 文件操作集（基础框架，可扩展open/read/write/release）

static struct file_operations cdev_test_ops = {

    .owner = THIS_MODULE,

};

  

// 3. 模块入口函数

static int modulecdev_init(void)

{

    int ret;

  

    // 动态申请1个次设备号的设备区域

    ret = alloc_chrdev_region(&dev_num, 0, 1, "alloc_cdev_test");

    if (ret < 0)

    {

        printk(KERN_ERR "alloc_chrdev_region failed, ret = %d\n", ret);

        return ret;

    }

    printk(KERN_INFO "alloc_chrdev_region success! major=%d, minor=%d\n",

           MAJOR(dev_num), MINOR(dev_num));

  

    // 初始化cdev结构体，绑定文件操作集

    cdev_test.owner = THIS_MODULE;

    cdev_init(&cdev_test, &cdev_test_ops);

  

    // 将cdev注册进内核，关联设备号

    ret = cdev_add(&cdev_test, dev_num, 1);

    if (ret < 0)

    {

        printk(KERN_ERR "cdev_add failed\n");

        // cdev_add失败要先释放设备号再退出

        unregister_chrdev_region(dev_num, 1);

        return ret;

    }

    printk(KERN_INFO "cdev_add register char device ok\n");

  

    return 0;

}

  

// 4. 模块出口函数

static void modulecdev_exit(void)

{

    // 注销顺序和注册相反：先删除cdev，再释放设备号

    cdev_del(&cdev_test);

    unregister_chrdev_region(dev_num, 1);

    printk(KERN_INFO "cdev unregister done, bye bye\n");

}

  

module_init(modulecdev_init);

module_exit(modulecdev_exit);

  

MODULE_LICENSE("GPL");

MODULE_AUTHOR("Embed Test");

MODULE_DESCRIPTION("Dynamic dev number + cdev register demo");

MODULE_VERSION("1.0");
