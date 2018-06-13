<img src="./images/logo_big.png" />

TypeORM 是一个[ORM](https://en.wikipedia.org/wiki/Object-relational_mapping),它可以运行在NodeJS,Browser,Cordova,PhoneGap,Ionic,React Native和Electron 平台并且可以和Typescript，Javascript(ES5,ES6,ES7)一起使用。它的目标是提供最新的JavaScript特性和提供额外的功能帮助你去开发任何使用数据库的应用 - 从只有一些表的小应用到巨大量级专业的多数据库应用。


TypeORM 全部支持活动记录和数据库映射模式，不像其他所有的当前已经存在的Javascript ORM，它意味着你可以用最高效的方式写出高质量，松散耦合，可扩展，可维护的应用在。

TypeORM 是受其他ORM高度影响，比如`Hibernate`,`Doctrine`和`Entity Framework`

一些TypeORM的特性
* 支持所有的数据映射和活动记录（你选择）
* 实体和列
* 数据库指定列类型
* 实体管理
* 存储库和自定义存储库
* 清洁对象关系模型
* 组合（关系）
* eager and lazy relations（急切和懒惰的关系）
* 单向，双向和自我引用关系
* 支持多继承模式
* 级联
* 索引
* 交易
* 迁移和自动迁移生成
* 链接池
* 复制
* 使用多数据库链接
* 和多数据库类型一起工作
* 跨数据库和跨模式查询
* 优雅的语法（elegant-syntax），灵活而强大的查询构建器
* 左和内链接
* 对使用链接的查询进行适当的分页
* 查询缓存
* 流媒体原始结果
* 日志
* 监听和订阅（钩子）
* 支持关闭表模式
* 模式声明在模型或者独立配置的文件中
* 链接配置在json/xml/yml/env formats
* 支持MySQL / MariaDB / Postgres / SQLite / Microsoft SQL Server / Oracle / sql.js
* 支持 MongoDB NoSQL数据库
* 在NodeJS / Browser / Ionic / Cordova / React Native / Electron 平台工作
* 支持Typescirpt 和Javascript
* 生产代码是高性能的，灵活的，简洁的，可维护的。
* 遵循所有的最佳实践
* CLI
还有更多

使用TypeORM 你的模型像这样
```javascript
import {Entity, PrimaryGeneratedColumn, Column} from "typeorm";

@Entity()
export class User {

    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    firstName: string;

    @Column()
    lastName: string;

    @Column()
    age: number;

}
```
并且你的域逻辑像这样
```javascript
const user = new User();
user.firstName = "Timber";
user.lastName = "Saw";
user.age = 25;
await repository.save(user);

const allUsers = await repository.find();
const firstUser = await repository.findOne(1); // find by id
const timber = await repository.findOne({ firstName: "Timber", lastName: "Saw" });

await repository.remove(timber);
```

另外，如果你倾向是使用`ActiveRecord`实现，你也可以使用它

```javascript
import {Entity, PrimaryGeneratedColumn, Column, BaseEntity} from "typeorm";

@Entity()
export class User extends BaseEntity {

    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    firstName: string;

    @Column()
    lastName: string;

    @Column()
    age: number;

}
```
并且，你的域逻辑将会像这种方式
```javascript
const user = new User();
user.firstName = "Timber";
user.lastName = "Saw";
user.age = 25;
await user.save();

const allUsers = await User.find();
const firstUser = await User.findOne(1);
const timber = await User.findOne({ firstName: "Timber", lastName: "Saw" });

await timber.remove();
```

# 安装
1.安装npm包
```shell
npm install typeorm --save
```
2.你需要安装`reflect-metadata`填充
```shell
npm install reflect-metadata --save
```
并且引入它在你应用全局的地方(举个例子在`app.ts`)
`import "reflect-metadata";`
3.你也许需要安装node类型
```shell
npm install @types/node --save
```
4.安装数据库驱动
* 对于 ***MySQL*** 或者 ***MariaDB*** `npm install mysql --save (你也可以安装mysql2)`

* 对于 ***PostgreSQL*** `npm install pg --save`

* 对于 ***SQLite*** `npm install sqlite3 --save`

* 对于 ***Microsoft SQL Server*** `npm install mssql --save`

* 对于 ***sql.js*** `npm install sql.js --save`

* 对于 ***Oracle*** `npm install oracledb --save`

安装他们其中一个依赖取决你数据库的使用。

为了使Oracle驱动工作，你需要遵循来自[他们](https://github.com/oracle/node-oracledb)网站的安装说明

* 对于 MongoDB (试验) `npm install mongodb --save`

# TypeScript 配置
确定你使用Typescript编译版本2.3或者更高，并且你已经在`tsconfig.json`文件中启用了以下设置
```json
"emitDecoratorMetadata": true,
"experimentalDecorators": true,
```
你也许需要启动`es6`在`lib`编译项中，或者安装来自于`@types`的`es6-shim`


# 快速开始
最快捷的使用TypeORM方式是使用它的CLI命令行去生成一个项目。仅当你使用NodeJS应用才能快速开始工作。如果你使用其他的平台，在[step-by-step 向导](http://typeorm.io/#/readme/step-by-step-guide)处理

首先，全局安装TypeORM

`npm install typeorm -g`

然后去你想要创建新项目的目录并且使用下面的命令

```shell
typeorm init --name MyProject --database mysql
```

其中`name`是你项目的名称并且`database`是你将要使用的数据库。数据库可以是下面值中的一个`mysql`, `mariadb`, `postgres`, `sqlite`, `mssql`, `oracle`, `mongodb`, `cordova`, `react-native`.

这个命令会生成一个新的项目和下面的文件在`MyProject`目录中
```
MyProject
    src                 // 是你ts代码的地方
        entity          // 你的实体（数据模型）存储的地方
            usr.ts      // 简单的实体
        migration       // 你的迁移存储的地方
        index.ts        // 开始你应用的地方
    .gitignore          // 标准的gitignore文件
    ormconfig.json      // ORM和数据库链接配置
    package.json        // node模块依赖
    README.md           // 简单的readme文件
    tsconfig.json       // typescript编译选项
```

你也可以运行`typeorm init`在已经存在的node项目，但是要注意有可能覆盖一些你已经拥有的文件

下一步是安装新项目的依赖
```shell
cd MyProject
npm install
```

在安装过程中，编辑`ormconfig.json`文件并且把你自己的数据库链接配置项放入这里
```json
{
   "type": "mysql",
   "host": "localhost",
   "port": 3306,
   "username": "test",
   "password": "test",
   "database": "test",
   "synchronize": true,
   "logging": false,
   "entities": [
      "src/entity/**/*.ts"
   ],
   "migrations": [
      "src/migration/**/*.ts"
   ],
   "subscribers": [
      "src/subscriber/**/*.ts"
   ]
}
```

尤其是，大部分时间你仅仅需要配置`host`,`username`,`password`,`database`也许`port`选项

一旦你完成了配置并且你的node模块已经安装，你可以运行你的应用

```shell
npm start
```

是的，你应用应该成功的运行并且插入一个新的用户在数据库中。你可以继续和这个项目以及持续集成的其他你需要的模块以及开始创建的更多实体一起工作。

你可以通过运行`typeorm init --name MyProject --database mysql --express`命令和express一起生成一个甚至更多高级的项目

# 分步指南
你对ORM有什么期望？首先，你期望它将会创建数据库的表并且可以查找，插入，更新，删除你的数据，而无需编写入大量难以维护的SQL查询。这个指南将会展现如果从头设置TypeORM并且创让它完成你对ORM的期望。

# 创建一个模型
和一个数据库开始从创建表一起工作。你如何告诉TypeORM去创建一个数据库表？答案是通过模型。在你系统中的模型是你数据库的表

举个例子,你有一个`Photo`模型
```javascript
export class Photo {
    id: number;
    name: string;
    description: string;
    filename: string;
    views: number;
}
```
并且你希望去存储相片在你的数据库。为了存储一些东西在数据库，首先你需要一个数据库表，并从创建自你模型的数据库表。不是所有模型，仅是那些你定义为实例的模型。

# 创建一个实体
实体是你模型通过`@Entity`装饰器装饰的。一个数据库表将会被模型创建。您可以使用TypeORM在任何地方使用实体。你可以load/insert/update/remove 并执行其他操作。

一起制造我们的`Photo`模型作为实体

```javascript
import {Entity} from "typeorm";

@Entity()
export class Photo {
    id: number;
    name: string;
    description: string;
    filename: string;
    views: number;
    isPublished: boolean;
}
```

现在，将`Photo`实体创建一个数据表，我们能够在我们应用程序的任何一个地方使用它。我们已经创建一个数据表，然而，表怎么能没有列的存在？一起创建一些列在我们的数据库表中。

# 增加表的列

增加数据库的列，你只需要用`@Column`装饰器将你想要创建的实体属性装饰成一列。

```javascript
import {Entity, Column} from "typeorm";

@Entity()
export class Photo {

    @Column()
    id: number;

    @Column()
    name: string;

    @Column()
    description: string;

    @Column()
    filename: string;

    @Column()
    views: number;

    @Column()
    isPublished: boolean;
}
```
现在，`id`,`name`,`description`,`filename`,`views`和`isPublished`列将被增加到`photo`表中。列类型在数据库是推到自你使用的属性类型，e.g. `number`将被转换成`integer`,`string`转换成`varchar`,`boolean`将转化为`bool`,等等。但是你可以使用任何你数据库支持的列类型通过隐式指定一个列类型在`@Column`装饰器中。

我们生成一个有列的数据库表，但是这还剩下一件事情。每一个数据库表必须有一个列是主键。

# 创建一个来主键列
每一个实体必须有至少一个主键列。这是必须的并且你不能避免。为了制造一个初见列。你需要使用`@PrimaryColumn`装饰器。

```javascript
import {Entity, Column, PrimaryColumn} from "typeorm";

@Entity()
export class Photo {

    @PrimaryColumn()
    id: number;

    @Column()
    name: string;

    @Column()
    description: string;

    @Column()
    filename: string;

    @Column()
    views: number;

    @Column()
    isPublished: boolean;
}
```

# 创建一个自动生成的列
现在，假设你希望你的id列能自动生成（这是众所周知的自动增加/连续/串行/生成标识列）。为了做到，你需要改变`@PrimaryColumn`装饰器成`@PrimaryGeneratedColumn`装饰器。

```javascript
import {Entity, Column, PrimaryGeneratedColumn} from "typeorm";

@Entity()
export class Photo {

    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    name: string;

    @Column()
    description: string;

    @Column()
    filename: string;

    @Column()
    views: number;

    @Column()
    isPublished: boolean;
}
```

# 列数据类型
接下来，一起修复我们的数据类型。默认，字符串映射成varchar(255)类似类型(依赖于数据库类型)。数字映射成integer类似的类型(依赖于数据库类型)。我们不希望我们所有的列成为varchar或者integers。一起设置正确的数据类型

```javascript
import {Entity, Column, PrimaryGeneratedColumn} from "typeorm";

@Entity()
export class Photo {

    @PrimaryGeneratedColumn()
    id: number;

    @Column({
        length: 100
    })
    name: string;

    @Column("text")
    description: string;

    @Column()
    filename: string;

    @Column("double")
    views: number;

    @Column()
    isPublished: boolean;
}
```

列类型是数据库指定的。你可以设置任何你数据库支持的列类型。更多支持列类型的信息你可以在[这里](http://typeorm.io/#/entities/column-types)找到

# 创建一个连接数据库的连接

现在，当我们的实体被创建，一起创建一个`index.ts`(或者`app.ts`随便你叫什么)文件并且设置我们的连接在那里

```javascript
import "reflect-metadata";
import {createConnection} from "typeorm";
import {Photo} from "./entity/Photo";

createConnection({
    type: "mysql",
    host: "localhost",
    port: 3306,
    username: "root",
    password: "admin",
    database: "test",
    entities: [
        Photo
    ],
    synchronize: true,
    logging: false
}).then(connection => {
    // here you can start to work with your entities
}).catch(error => console.log(error));
```

我们使用MySQL在这个例子中，但是你可以使用任何支持的数据库。为了使用其他的数据库，简单的改变在选项中`type`，改成你正在使用的数据库mysql, mariadb, postgres, sqlite, mssql, oracle, cordova, react-native or mongodb。另外确定你自己的主机，端口，用户名，密码和数据库设置。

我们增加我们的Photo实体在这个链接的实体列表中。每一个你使用的实体都必须在链接的列表中。

设置`synchronize`确定你的实体将会同步数据库，在每一次你运行应用时。

# 从文件夹中加载所有的实体
往后，当你创建更多的实体我们需要去增加他们到我们的配置中。这不是很方便，所以我们可以设置整个文件夹，来自文件夹的所有实体将会链接并且在我们的链接中使用。


```javascript
import {createConnection} from "typeorm";

createConnection({
    type: "mysql",
    host: "localhost",
    port: 3306,
    username: "root",
    password: "admin",
    database: "test",
    entities: [
        __dirname + "/entity/*.js"
    ],
    synchronize: true,
}).then(connection => {
    // here you can start to work with your entities
}).catch(error => console.log(error));
```

这个途径需要注意。如果你使用了`ts-node`你需要去指定`.ts`文件的路径。如果你使用`outDir`你讲需要指定`.js`文件在`outDir`文件夹中的路径。如果你使用`outDir`并且当你删除或者重命名你的实体，确定去清除`outDir`文件夹并且重编译你的项目。因为当你删除你的源`.ts`文件他编译的`.js`版本不会被移除在ouput文件夹中并且任然通过TypeORM加载，因为他们当下在`outDir`文件夹中。


# 运行应用

现在如果你运行你的`index.ts`一个使用数据库的连接将会被初始化，并且你的photo数据库表将会被创建

```
+-------------+--------------+----------------------------+
|                         photo                           |
+-------------+--------------+----------------------------+
| id          | int(11)      | PRIMARY KEY AUTO_INCREMENT |
| name        | varchar(500) |                            |
| description | text         |                            |
| filename    | varchar(255) |                            |
| views       | int(11)      |                            |
| isPublished | boolean      |                            |
+-------------+--------------+----------------------------+
```

# 往数据库创建并且插入一张照片

现在，一起在数据库创建新的照片去保存它：

```javascript
import {createConnection} from "typeorm";
import {Photo} from "./entity/Photo";

createConnection(/*...*/).then(connection => {

    let photo = new Photo();
    photo.name = "Me and Bears";
    photo.description = "I am near polar bears";
    photo.filename = "photo-with-bears.jpg";
    photo.views = 1;
    photo.isPublished = true;

    return connection.manager
            .save(photo)
            .then(photo => {
                console.log("Photo has been saved. Photo id is", photo.id);
            });

}).catch(error => console.log(error));
```

一旦你的实体被保存将会得到新生成的id。`save`方法返回一个和你传递的数据一样的对象。它不是新复制的对象，它修改photo的"id"并且返回了它。

# 使用 async/await 语法

一起利用最新的ES7特性并且使用async/await语法来代替

```javascript
import {createConnection} from "typeorm";
import {Photo} from "./entity/Photo";

createConnection(/*...*/).then(async connection => {

    let photo = new Photo();
    photo.name = "Me and Bears";
    photo.description = "I am near polar bears";
    photo.filename = "photo-with-bears.jpg";
    photo.views = 1;
    photo.isPublished = true;

    await connection.manager.save(photo);
    console.log("Photo has been saved");

}).catch(error => console.log(error));
```

# 使用实体管理

我们仅仅创建一个新的photo并且保存它在数据库中。我们使用`EntityManager`去保存它。使用实体管理你可以维护任何在你应用中的实体。举个例子，一起加在我们的保存的实体。

```javascript
import {createConnection} from "typeorm";
import {Photo} from "./entity/Photo";

createConnection(/*...*/).then(async connection => {

    /*...*/
    let savedPhotos = await connection.manager.find(Photo);
    console.log("All photos from the db: ", savedPhotos);

}).catch(error => console.log(error));
```

`savedPhotos`将会成为一个加载自数据库中的数组对象

学习更多实体管理在[这里](http://typeorm.io/#/working-with-entity-manager/)

# 使用存储库
现在，一起重构我们的代码使用`Repository`代替`EntityManager`。每一个实体有自己的存储库处理他们的实体的所有操作。当你处理很多实体。存储库是比实体管理更方便的。

```javascript
import {createConnection} from "typeorm";
import {Photo} from "./entity/Photo";

createConnection(/*...*/).then(async connection => {

    let photo = new Photo();
    photo.name = "Me and Bears";
    photo.description = "I am near polar bears";
    photo.filename = "photo-with-bears.jpg";
    photo.views = 1;
    photo.isPublished = true;

    let photoRepository = connection.getRepository(Photo);

    await photoRepository.save(photo);
    console.log("Photo has been saved");

    let savedPhotos = await photoRepository.find();
    console.log("All photos from the db: ", savedPhotos);

}).catch(error => console.log(error));
```

更多关于存储库在[这里](http://typeorm.io/#/working-with-repository/)

# 加载数据库

一起尝试使用存储库的更多加载操作
```javascript
import {createConnection} from "typeorm";
import {Photo} from "./entity/Photo";

createConnection(/*...*/).then(async connection => {

    /*...*/
    let allPhotos = await photoRepository.find();
    console.log("All photos from the db: ", allPhotos);

    let firstPhoto = await photoRepository.findOne(1);
    console.log("First photo from the db: ", firstPhoto);

    let meAndBearsPhoto = await photoRepository.findOne({ name: "Me and Bears" });
    console.log("Me and Bears photo from the db: ", meAndBearsPhoto);

    let allViewedPhotos = await photoRepository.find({ views: 1 });
    console.log("All viewed photos: ", allViewedPhotos);

    let allPublishedPhotos = await photoRepository.find({ isPublished: true });
    console.log("All published photos: ", allPublishedPhotos);

    let [allPhotos, photosCount] = await photoRepository.findAndCount();
    console.log("All photos: ", allPhotos);
    console.log("Photos count: ", photosCount);

}).catch(error => console.log(error));
```

# 更新数据库

现在，一起加载数据库中的单独照片，更新它，保存它。

```javascript
import {createConnection} from "typeorm";
import {Photo} from "./entity/Photo";

createConnection(/*...*/).then(async connection => {

    /*...*/
    let photoToUpdate = await photoRepository.findOne(1);
    photoToUpdate.name = "Me, my friends and polar bears";
    await photoRepository.save(photoToUpdate);

}).catch(error => console.log(error));
```
现在，数据库中照片id为1将会被更新

# 删除来自数据库的数据

现在，一起删除数据库中我们的照片

```javascript
import {createConnection} from "typeorm";
import {Photo} from "./entity/Photo";

createConnection(/*...*/).then(async connection => {

    /*...*/
    let photoToRemove = await photoRepository.findOne(1);
    await photoRepository.remove(photoToRemove);

}).catch(error => console.log(error));
```

# 创建一对一的关系
一起在另一类中创建一个一对一的关系。一起创建一个新的类`PhotoMetadata.ts`这个PhotoMetadata类应该包含我们照片额外信息。

```javascript
import {Entity, Column, PrimaryGeneratedColumn, OneToOne, JoinColumn} from "typeorm";
import {Photo} from "./Photo";

@Entity()
export class PhotoMetadata {

    @PrimaryGeneratedColumn()
    id: number;

    @Column("int")
    height: number;

    @Column("int")
    width: number;

    @Column()
    orientation: string;

    @Column()
    compressed: boolean;

    @Column()
    comment: string;

    @OneToOne(type => Photo)
    @JoinColumn()
    photo: Photo;
}
```
这里，我们使用一个新的装饰器`@OneToOne`。它允许我们去创建一个一对一关系在两个实体之间。`type => Photo`是一个函数，它返回这个实体类和我们想要建立我们的关系的。我们被迫使用这个方法返回一个类，而不是直接使用类，因为具体的语言，我们也可以写成`() => Photo`，但我们使用`type => Photo`作为一个约定来提高代码可读性。这个类型变量它自己不包含任何东西。

我们增加了`@JoinColumn`装饰器，它指示这边的关系将拥有这个关系。关系可以是单向或者双向的。只有关系的一方可以拥有。在我们拥有的这方使用`@JoinColumn`装饰器是必要的。

如果你运行应用，你将会看到新生成的表，并且他将会包含一个外键是photo关系的列。

```
+-------------+--------------+----------------------------+
|                     photo_metadata                      |
+-------------+--------------+----------------------------+
| id          | int(11)      | PRIMARY KEY AUTO_INCREMENT |
| height      | int(11)      |                            |
| width       | int(11)      |                            |
| comment     | varchar(255) |                            |
| compressed  | boolean      |                            |
| orientation | varchar(255) |                            |
| photoId     | int(11)      | FOREIGN KEY                |
+-------------+--------------+----------------------------+
```

# 保存一对一关系

现在，一起保存photo，他的元数据并将他们互相连接

```javascript
import {createConnection} from "typeorm";
import {Photo} from "./entity/Photo";
import {PhotoMetadata} from "./entity/PhotoMetadata";

createConnection(/*...*/).then(async connection => {

    // create a photo
    let photo = new Photo();
    photo.name = "Me and Bears";
    photo.description = "I am near polar bears";
    photo.filename = "photo-with-bears.jpg";
    photo.isPublished = true;

    // create a photo metadata
    let metadata = new PhotoMetadata();
    metadata.height = 640;
    metadata.width = 480;
    metadata.compressed = true;
    metadata.comment = "cybershoot";
    metadata.orientation = "portait";
    metadata.photo = photo; // this way we connect them

    // get entity repositories
    let photoRepository = connection.getRepository(Photo);
    let metadataRepository = connection.getRepository(PhotoMetadata);

    // first we should save a photo
    await photoRepository.save(photo);

    // photo is saved. Now we need to save a photo metadata
    await metadataRepository.save(metadata);

    // done
    console.log("Metadata is saved, and relation between metadata and photo is created in the database too");

}).catch(error => console.log(error));
```

# 关系的反面

关系可以是单向的或者双向的。当前，我们的关系在PhotoMetadata 和 Photo 之间是单向的，并且Photo不知道任何关于PhotoMetadata的事情。这使得从Photo这一侧访问PhotoMetadata变的复杂。为了修复这个问题women那应该增加反向关系，并且让PhotoMetadata和Photo双向关联。一起去修改我们的实体

```javascript
import {Entity, Column, PrimaryGeneratedColumn, OneToOne, JoinColumn} from "typeorm";
import {Photo} from "./Photo";

@Entity()
export class PhotoMetadata {

    /* ... other columns */

    @OneToOne(type => Photo, photo => photo.metadata)
    @JoinColumn()
    photo: Photo;
}
```
```javascript
import {Entity, Column, PrimaryGeneratedColumn, OneToOne} from "typeorm";
import {PhotoMetadata} from "./PhotoMetadata";

@Entity()
export class Photo {

    /* ... other columns */

    @OneToOne(type => PhotoMetadata, photoMetadata => photoMetadata.photo)
    metadata: PhotoMetadata;
}
```
`photo => photo.metadata`是一个函数，它返回关系的反面的名字。这里我们展示这个在Photo类的元数据属性，在Photo类，我们存储PhotoMetadata。而不是一个photo属性。你可以简单的改变传递一个字符串给`@OneToOne`装饰器，就像`metadata`。但我们使用这个函数类型的途径让我们重构变的简单。

提醒我们应该使用`@JoinColumn`装饰器仅仅在一面的关系。任何你放入这个装饰器的面将会变成我们这面的关系。这个关系拥有者包含一个外键的列在数据库中。

# 用对象加载对象
现在，一起加载我们的photo和他的photometadata在单独的查询中。这有两种方式去完成。使用`find * `方法或者使用`QueryBuilder`方法。首先一起使用`find *`。`find *`方法允许你去使用`FindOneOptions` / `FindManyOptions`接口指定的对象。

```javascript
import {createConnection} from "typeorm";
import {Photo} from "./entity/Photo";
import {PhotoMetadata} from "./entity/PhotoMetadata";

createConnection(/*...*/).then(async connection => {

    /*...*/
    let photoRepository = connection.getRepository(Photo);
    let photos = await photoRepository.find({ relations: ["metadata"] });

}).catch(error => console.log(error));
```

这里，photos将包含一个来自数据库的照片数组，并且每一个照片将包含它照片的元数据。更多查找选项在[这个文档中](http://typeorm.io/#/find-options/)

使用查找选项是好的并且简单的。但是如果你需要更复杂的查询，你应该使用`QueryBuilder`。`QueryBuilder`允许更复杂的查询是一种优雅的方式。

```javascript
import {createConnection} from "typeorm";
import {Photo} from "./entity/Photo";
import {PhotoMetadata} from "./entity/PhotoMetadata";

createConnection(/*...*/).then(async connection => {

    /*...*/
    let photos = await connection
            .getRepository(Photo)
            .createQueryBuilder("photo")
            .innerJoinAndSelect("photo.metadata", "metadata")
            .getMany();


}).catch(error => console.log(error));
```

`QueryBuilder`允许创建并且执行几乎任何复杂的SQL查询。当你和`QueryBuilder`一起工作，想想你创建一个SQL查询。在这个例子，photo和metadata是别名应用在选择photos中。你使用别名访问列和选择数据的属性。

# 使用级联自动保存相关对象
我们设置级联选项在我们的关系。在这个例子，当你希望我们的关系对象在其他对象被保存时能被保存。一起改变一点我们的`@OneToOne`装饰器

```javascript
export class Photo {
    /// ... other columns

    @OneToOne(type => PhotoMetadata, metadata => metadata.photo, {
        cascade: true,
    })
    metadata: PhotoMetadata;
}
```

使用`cascade`允许我们不单独保存photo和单独保存metadata对象。现在，我们可以简单的保存photo对象，并且这个metadata对象因为级联选项也将会自动保存。

```javascript
createConnection(options).then(async connection => {

    // create photo object
    let photo = new Photo();
    photo.name = "Me and Bears";
    photo.description = "I am near polar bears";
    photo.filename = "photo-with-bears.jpg";
    photo.isPublished = true;

    // create photo metadata object
    let metadata = new PhotoMetadata();
    metadata.height = 640;
    metadata.width = 480;
    metadata.compressed = true;
    metadata.comment = "cybershoot";
    metadata.orientation = "portait";

    photo.metadata = metadata; // this way we connect them

    // get repository
    let photoRepository = connection.getRepository(Photo);

    // saving a photo also save the metadata
    await photoRepository.save(photo);

    console.log("Photo is saved, photo metadata is saved too.")

}).catch(error => console.log(error));
```

# 创建多对一/一对多关系

一起创建多对一/一对多关系。假设一个照片有一个作者，每个作者有很多照片。首先，一起创建`Author`类

```javascript
import {Entity, Column, PrimaryGeneratedColumn, OneToMany, JoinColumn} from "typeorm";
import {Photo} from "./Photo";

@Entity()
export class Author {

    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    name: string;

    @OneToMany(type => Photo, photo => photo.author) // note: we will create author property in the Photo class below
    photos: Photo[];
}
```

`Author`包含关系的反面。`OneToMany`总是关系的反面，没有`ManyToOne`在关系的另一面，它就不能存在。

现在一起增加自己的关系面在photo实体

```javascript
import {Entity, Column, PrimaryGeneratedColumn, ManyToOne} from "typeorm";
import {PhotoMetadata} from "./PhotoMetadata";
import {Author} from "./Author";

@Entity()
export class Photo {

    /* ... other columns */

    @ManyToOne(type => Author, author => author.photos)
    author: Author;
}
```

在 many-to-one / one-to-many 关系中，拥有者的面总是many-to-one。它意味着使用`@ManyToOne`将会存储关系对象的id的类。

在你运行应用之后，ORM将会创建`author`表
```
+-------------+--------------+----------------------------+
|                          author                         |
+-------------+--------------+----------------------------+
| id          | int(11)      | PRIMARY KEY AUTO_INCREMENT |
| name        | varchar(255) |                            |
+-------------+--------------+----------------------------+
```

它也将修改`photo`表，增加`author`列并且创建一个外键给这个列
```
+-------------+--------------+----------------------------+
|                         photo                           |
+-------------+--------------+----------------------------+
| id          | int(11)      | PRIMARY KEY AUTO_INCREMENT |
| name        | varchar(255) |                            |
| description | varchar(255) |                            |
| filename    | varchar(255) |                            |
| isPublished | boolean      |                            |
| authorId    | int(11)      | FOREIGN KEY                |
+-------------+--------------+----------------------------+
```

# 创建多对多关系
一起创建many-to-one / many-to-many 关系。假设一个photo在很多专辑中。并且每一个专辑包含很多照片。一起创建`Album`类

```javascript
import {Entity, PrimaryGeneratedColumn, Column, ManyToMany, JoinTable} from "typeorm";

@Entity()
export class Album {

    @PrimaryGeneratedColumn()
    id: number;

    @Column()
    name: string;

    @ManyToMany(type => Photo, photo => photo.albums)
    @JoinTable()
    photos: Photo[];
}
```

`@JoinTable`是必须的去指定这个拥有者的关系面。

现在，一起增加我们关系的反面给photo类

```javascript
export class Photo {
    /// ... other columns

    @ManyToMany(type => Album, album => album.photos)
    albums: Album[];
}
```

在你运行完应用后，ORM将会创建`album_photos_photo_albums`连接点表
```
+-------------+--------------+----------------------------+
|                album_photos_photo_albums                |
+-------------+--------------+----------------------------+
| album_id    | int(11)      | PRIMARY KEY FOREIGN KEY    |
| photo_id    | int(11)      | PRIMARY KEY FOREIGN KEY    |
+-------------+--------------+----------------------------+
```

不要忘记注册`Album`类和你的连接在ORM

```javascript
const options: ConnectionOptions = {
    // ... other options
    entities: [Photo, PhotoMetadata, Author, Album]
};
```

现在，一起插入ablums和photos 给我们的数据库
```javascript
let connection = await createConnection(options);

// create a few albums
let album1 = new Album();
album1.name = "Bears";
await connection.manager.save(album1);

let album2 = new Album();
album2.name = "Me";
await connection.manager.save(album2);

// create a few photos
let photo = new Photo();
photo.name = "Me and Bears";
photo.description = "I am near polar bears";
photo.filename = "photo-with-bears.jpg";
photo.albums = [album1, album2];
await connection.manager.save(photo);

// now our photo is saved and albums are attached to it
// now lets load them:
const loadedPhoto = await connection
    .getRepository(Photo)
    .findOne(1, { relations: ["albums"] });
```

`loadedPhoto`将会等价于

```json
{
    id: 1,
    name: "Me and Bears",
    description: "I am near polar bears",
    filename: "photo-with-bears.jpg",
    albums: [{
        id: 1,
        name: "Bears"
    }, {
        id: 2,
        name: "Me"
    }]
}
```

# 使用QueryBuilder

你可以使用QueryBuilder去构建大部分复杂的SQL查询。举个例子，你看这样做
```javascript
let photos = await connection
    .getRepository(Photo)
    .createQueryBuilder("photo") // first argument is an alias. Alias is what you are selecting - photos. You must specify it.
    .innerJoinAndSelect("photo.metadata", "metadata")
    .leftJoinAndSelect("photo.albums", "album")
    .where("photo.isPublished = true")
    .andWhere("(photo.name = :photoName OR photo.name = :bearName)")
    .orderBy("photo.id", "DESC")
    .skip(5)
    .take(10)
    .setParameters({ photoName: "My", bearName: "Mishka" })
    .getMany();
```

这个选择查询所有名字为"My"或者"Mishaka"的发布的照片。它将会选择结果从位置5（分页偏移），并且将选择只有10个结果（分页限制）。这个选择结果将会通过id降序排列。这个photo的albums将会左连接并且他们的metadata将会内连接。

你将使用查询构建起在你的应用中。学习更多关于QueryBuilder在[这里](http://typeorm.io/#/select-query-builder/)

# 例子

查看样本中的样本以查看使用[示例](https://github.com/typeorm/typeorm/tree/master/sample)。

这里有一些你可以克隆并且开始使用库

* [Example how to use TypeORM with TypeScript](https://github.com/typeorm/typescript-example)
* [Example how to use TypeORM with JavaScript](https://github.com/typeorm/javascript-example)
* [Example how to use TypeORM with JavaScript and Babel](https://github.com/typeorm/babel-example)
* [Example how to use TypeORM with TypeScript and SystemJS in Browser](https://github.com/typeorm/browser-example)
* [Example how to use Express and TypeORM](https://github.com/typeorm/typescript-express-example)
* [Example how to use Koa and TypeORM](https://github.com/typeorm/typescript-koa-example)
* [Example how to use TypeORM with MongoDB](https://github.com/typeorm/mongo-typescript-example)
* [Example how to use TypeORM in a Cordova/PhoneGap app](https://github.com/typeorm/cordova-example)
* [Example how to use TypeORM with an Ionic app](https://github.com/typeorm/ionic-example)
* [Example how to use TypeORM with React Native](https://github.com/typeorm/react-native-example)
* [Example how to use TypeORM with Electron using JavaScript](https://github.com/typeorm/electron-javascript-example)
* [Example how to use TypeORM with Electron using TypeScript](https://github.com/typeorm/electron-typescript-example)

# 扩展

这有一些扩展，它可以简单和TypeORM一起工作并且集成其他的模块。

* [TypeORM + GraphQL framework](http://vesper-framework.com)
* [TypeORM integration](https://github.com/typeorm/typeorm-typedi-extensions) with [TypeDI](https://github.com/typestack/typedi)
* [TypeORM integration](https://github.com/typeorm/typeorm-routing-controllers-extensions) with [routing-controllers](https://github.com/typestack/routing-controllers)
Models generation from existing database - [typeorm-model-generator](https://github.com/Kononnable/typeorm-model-generator)


# 原文地址
[地址](http://typeorm.io/#/)

