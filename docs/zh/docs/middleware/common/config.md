# 配置管理

配置管理功能提供了对象存储的通用配置方案，用于各中间件实例的数据备份与恢复，具体配置方式如下。

1. 点击 __配置管理__， 进入 __配置管理__ 列表；

    ![list](https://docs.daocloud.io/daocloud-docs-images/docs/zh/docs/middleware/common/images/cfg01.png)

2. 点击 __创建__ 在配置管理页面中创建一个新的配置项；

    ![list](https://docs.daocloud.io/daocloud-docs-images/docs/zh/docs/middleware/common/images/cfg02.png)

3. 在创建页面中，配置如下内容：

    ![list](https://docs.daocloud.io/daocloud-docs-images/docs/zh/docs/middleware/common/images/s3config.png)

    - **名称** ：用户自定义，用于标示配置项；

    - **备份类型** ：该配置具有两个选项，默认为 __托管 MinIO__，将在列表中展示所有中间件 MinIO 列表中的实例；选择 __S3__ 可使用外部存储，用户需要自行输入外部存储的地址，地址结构类似：`http://172.30.120.201:30456`

    - **Access_Key、Secret_Key** ：该项需要在 MinIO 的管理页面中获取，步骤如下：

        1. 在 MinIO 实例中点击访问地址进入管理界面；

            ![list](https://docs.daocloud.io/daocloud-docs-images/docs/zh/docs/middleware/common/images/cfg04.png)

        2. 点击 __Identity__ -> __Service Account__ ，创建一个新的 __Service Account__ ；

            ![list](https://docs.daocloud.io/daocloud-docs-images/docs/zh/docs/middleware/common/images/cfg05.png)

        3. 把此处创建的 __Access_Key__ 和 __Secret_Key__ 复制到创建配置页面。

            ![list](https://docs.daocloud.io/daocloud-docs-images/docs/zh/docs/middleware/common/images/cfg06.png)

    - **Bucket 名称** ：该名称用于定义备份所需的对象存储桶，可在MinIO管理平台中获取，如下图所示：

        ![list](https://docs.daocloud.io/daocloud-docs-images/docs/zh/docs/middleware/common/images/cfg07.png)

4. 点击 __确定__ 完成创建，该配置将可用于中间件的 __备份/恢复__ 。

    ![list](https://docs.daocloud.io/daocloud-docs-images/docs/zh/docs/middleware/common/images/cfg08.png)
