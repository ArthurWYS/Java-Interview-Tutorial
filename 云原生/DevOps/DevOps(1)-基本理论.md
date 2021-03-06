# 1 辨析敏捷/持续集成/持续交付/DevOps
![](https://img-blog.csdnimg.cn/2020091822592454.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzNTg5NTEw,size_16,color_FFFFFF,t_70#pic_center)

# 2 持续集成

## 2.1 为何会有持续集成？
敏捷开发解决了单体应用的开发和每日构建的问题。

而单体应用拆分成微服务，就需要有一套方案来组装这些微服务，使其成为可协作运行的微服务架构。该方案就是持续集成。

- 持续集成强调开发人员提交新代码后，立刻进行构建、（单元）测试。根据测试结果，可确定新代码和原有代码是否正确集成在一起。
![](https://img-blog.csdnimg.cn/20200919010053171.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzNTg5NTEw,size_16,color_FFFFFF,t_70#pic_center)


## 2.2 持续集成的定义
持续交付的鼻祖Martin Fowler提出：持续集成(Continous Integration)是一种软件开发实践，帮助团队成员频繁集成他们的工作，通常每个项目每天至少集成一次，从而每天有可测试的版本。
每次集成使用自动化构建(含测试)来实现打包和测试，快速验证问题。许多团队发现持续集成显著地降低了集成遇到的错误，使团队能够更加迅速地开发软件。

## 2.3 为何需要持续集成![](https://img-blog.csdnimg.cn/20200919001633283.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzNTg5NTEw,size_16,color_FFFFFF,t_70#pic_center)
就如同Git是为了把代码集成在一起管理，持续构建就是把功能集成在一起，保证编译不出错。
类似的还有自动化测试保证一个模块的功能集成在一起能够正确工作。
联调测试环境则能将不同模块之间集成在一起，在一个类生产的环境中进行测试。

## 2.4 持续集成流水线的设计
![](https://img-blog.csdnimg.cn/20200919005133257.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzNTg5NTEw,size_16,color_FFFFFF,t_70#pic_center)

# 3 持续部署

## 3.1 传统部署的缺陷
- 传统部署部署方式严重依赖手工部署，人力成本高
- 生产环境依赖手工配置进行变更，非常繁琐
- 熬夜加班进行上线部署，效率很低

## 3.2 持续部署的定义
首先明确概念，软件部署：将软件按期望状态部署到目标机器的期望路径。

持续部署：自动化的将一或多个软件尽可能快的、稳定的、可重复的联合部署到目标机器，以便软件功能的验证和实际运行。
可能是在云环境中自动部署、app升级(如手机上的应用程序)、更新网站或只更新可用版本列表。
- 持续部署是在持续交付基础上，将部署到生产环境这一过程自动化。

![](https://img-blog.csdnimg.cn/20200919010019776.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzNTg5NTEw,size_16,color_FFFFFF,t_70#pic_center)
## 3.3 持续部署的基本要素
- 自动化部署 - ansible
- 应用与配置分离，一次构建，多处运行 - Spring Cloud Config
- 提供应用健康监测的接口 - Spring Cloud Actuator

## 3.4 常见自动化部署方法
![](https://img-blog.csdnimg.cn/20200919011237162.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzNTg5NTEw,size_16,color_FFFFFF,t_70#pic_center)
其中的vault专门用于存储一些加密信息，比如用户密码

## 3.5 测试部署效果

### 蓝绿部署（Blue-Green Deployment）
一种应用发布模式，可将用户流量从先前版本的应用或微服务逐渐转移到几乎相同的新版本中（两者均保持在生产环境中运行）。

该种部署软件的方法中，维护两个相同的主机环境
- 蓝色
旧版本的生产环境
- 绿色
新版本的预发布环境

一旦生产流量从蓝色完全转移到绿色，蓝色就可在回滚或退出生产的情况下保持待机，也可更新成为下次更新的模板。

自动化部署面临的挑战之一是转换本身，将软件从测试的最后阶段转移到实际生产中。通常，您需要快速执行此操作，以最大程度减少停机时间。蓝绿部署方法通过确保拥有两个尽可能相同的生产环境来做到这一点。
在任何时候，其中一个（例如蓝色）都处于活动状态。准备新版本的软件时，在绿色环境中进行最后的测试阶段。一旦软件在绿色环境中运行，就可以切换路由器，以便所有传入请求都进入绿色环境-蓝色的请求现在处于空闲状态。

蓝绿部署还提供了快速回滚的方法-如果出现任何问题，将路由切换回蓝色环境。
在绿色环境处于活动状态时，仍然存在处理丢失的事务的问题，你可能能够以在绿色环境处于活动状态时将蓝色环境作为备份的方式向这两个环境提供交易。或者，您可以在切换前将应用程序置于只读模式，以只读模式运行一段时间，然后将其切换为读写模式。这可能足以清除许多未解决的问题。
**两种环境必须不同，但要尽可能相同**。在某些情况下，它们可以是不同的硬件，也可以是在相同（或不同）硬件上运行的不同虚拟机。它们也可以是一个单独的操作环境，分为两个区域，两个区域具有单独的IP地址。
将绿色环境投入使用并对它的稳定性感到满意之后，就可以将蓝色环境用作过渡环境，以进行下一个部署的最后测试步骤。准备好发布下一个版本时，你从绿色切换为蓝色的方式与之前从蓝色切换为绿色的方式相同。这样，绿色和蓝色环境便会定期在实时上一个版本（用于回滚）和下一个新版本之间进行循环。
这种方法的一个优点是，它与获得热备份工作所需的基本机制相同。因此，这使您可以在每个版本上测试灾难恢复过程。 （我希望你发布的时间比灾难多得多。）基本思想是要在两个易于切换的环境之间进行切换，有很多方法可以更改细节。一个项目通过跳动Web服务器而不是在路由器上工作来进行切换。另一种变化是使用相同的数据库，从而为Web和域层设置了蓝绿色的开关。使用这种技术，数据库通常可能是一个挑战，尤其是当您需要更改架构以支持软件的新版本时。技巧是将架构更改的部署与应用程序升级分开。因此，首先应用数据库重构来更改架构以支持应用程序的新旧版本，进行部署，检查一切是否正常，以便您有一个回滚点，然后部署该应用程序的新版本。 （并且在升级失败后，删除对旧版本的数据库支持。）

该技术已经存在了很长时间了，但是Martin Fowler并不认为它应该经常使用。 Daniel Terhorst-North和Jez Humble的一些模糊组合提出了这个名称。

这种持续部署模式原本存在不足之处。并非所有环境都具有相同的正常运行时间要求或正确执行 CI/CD 流程（如蓝绿部署）所需的资源。但是，随着企业加大对数字化转型的支持，许多应用开始支持这种。
#### 模型图
在这些实例的前面是调度系统，它们充当产品或应用程序的客户“网关”。通过将调度系统指向蓝色或绿色实例,可以将客户流量引流到期望的部署环境。通过这种方式，切换指向哪个部署实例(蓝色或绿色)对用户来说是快速简单而透明的。
![](https://img-blog.csdnimg.cn/20200919014805478.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzNTg5NTEw,size_16,color_FFFFFF,t_70#pic_center)

### 金丝雀部署（灰度发布）
一部分客户流量被重新引流到新的版本部署中。例如，新版本的搜索服务可与当前服务的生产版本一起部署。
然后，可将10%的搜索查询引流到新版本，以在生产环境中对其进行测试。

如果服务那些流量的新版本没问题，那么可能会有更多流量会被逐渐引流过去。如果仍然没有问题出现，那么随时间推移，可对新版本增量部署，直到100%的流量都调度到新版本。
#### 模型图
![](https://img-blog.csdnimg.cn/2020091902172417.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzNTg5NTEw,size_1,color_FFFFFF,t_70#pic_center)

### 暗发布（DarkLaunching）
也叫功能开关，指软件特性在正式发布之前，先将其第一个版本部署到生产环境。通过应用“开关”技术，使用户在无感的情况下应用新特性的功能，软件提供商通过收集用户的实际操作记录来获得针对这个新特性的反馈数据。
当然，发布新特性，使用户无感还是比较难做到的。新特性所针对软件的改变通常不体现在用户经常使用的界面按钮的调整，更多的是后台交易逻辑或算法层面的调整。

对于可能需要轻松关掉的新功能(若发现有问题)，开发人员可添加功能开关(feature toggles)。这是代码中的if-then软件功能开关，仅在设置数据值时才激活新代码。
- 此数据值可以是全可访问的位置，部署的应用程序将检查该位置是否应执行新代码。如果设置了数据值，则执行代码；如果没有，则不执行。
- 这为开发人员提供了一个远程“终止开关”，以便在部署到生产环境后发现问题时关闭新功能。
![](https://img-blog.csdnimg.cn/2020091904225939.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzNTg5NTEw,size_16,color_FFFFFF,t_70#pic_center)

#### 案例
某互联网公司重新开发了一个在线新闻推荐算法，希望能够为其用户推荐更多和更好的新闻内容。但是，由于此算法相对于以前算法的复杂度较高，提供算法的公司需要搜集该算法的执行效果。基于这种需求，我们就可以应用暗部署的方法。我们可以为这个算法配置一个开关，并将其部署到生产环境中。当针对这个算法的开关打开时，用户的访问流浪就会触发这个新算法的执行。通常用户并不知道其此次访问所调用的算法的新旧。如果这个算法在大规模用户并发情况下的性能不好，我们就可以马上关闭这个算法所对应的开关，让用户使用原来的算法。

参考
- https://www.mindtheproduct.com/what-the-hell-are-ci-cd-and-devops-a-cheatsheet-for-the-rest-of-us/
- https://tech.youzan.com/gray-deloyments-and-blue-green-deployments-practices-in-youzan/
- http://stormluke.me/deploy-not-equal-release-part-one/
- https://martinfowler.com/bliki/BlueGreenDeployment.html