# Kogito message node bug
This repo is a demo of an issue I've been experiencing with BPM Messaging Nodes in Kogito/Quarkus

## Description of issue
I have a process with two Message Nodes of the same type. As far I know, this is valid BPMN. However, the application 
fails to build. If I remove a message node, it builds and runs just fine.

The error message I get is:

```
java.lang.RuntimeException: io.quarkus.builder.BuildException: Build failure: Build failed due to errors
        [error]: Build step io.quarkus.arc.deployment.ArcProcessor#validate threw an exception: javax.enterprise.inject.spi.DeploymentException: javax.enterprise.inject.UnsatisfiedResolutionException: Unsatisfied dependency for type org.kie.kogito.event.EventEmitter and qualifiers [@Default]
        - java member: com.jongunter.TestMessageProducer_1#emitter
        - declared on CLASS bean [types=[com.jongunter.TestMessageProducer_1, org.kie.kogito.services.event.impl.AbstractMessageProducer<java.lang.String, com.jongunter.TestMessageDataEvent_1>, java.lang.Object], qualifiers=[@Default, @Any], target=com.jongunter.TestMessageProducer_1]
        The following beans match by type, but none have matching qualifiers:
                - Bean [class=org.kie.kogito.app.HelloworldEventEmitter, qualifiers=[@HelloworldQualifier, @Any]]
        at io.quarkus.arc.processor.BeanDeployment.processErrors(BeanDeployment.java:1202)
        at io.quarkus.arc.processor.BeanDeployment.init(BeanDeployment.java:272)
        at io.quarkus.arc.processor.BeanProcessor.initialize(BeanProcessor.java:134)
        at io.quarkus.arc.deployment.ArcProcessor.validate(ArcProcessor.java:462)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:77)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.base/java.lang.reflect.Method.invoke(Method.java:568)
        at io.quarkus.deployment.ExtensionLoader$2.execute(ExtensionLoader.java:882)
        at io.quarkus.builder.BuildContext.run(BuildContext.java:277)
        at org.jboss.threads.ContextHandler$1.runWith(ContextHandler.java:18)
        at org.jboss.threads.EnhancedQueueExecutor$Task.run(EnhancedQueueExecutor.java:2449)
        at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.run(EnhancedQueueExecutor.java:1478)
        at java.base/java.lang.Thread.run(Thread.java:833)
        at org.jboss.threads.JBossThread.run(JBossThread.java:501)
Caused by: javax.enterprise.inject.UnsatisfiedResolutionException: Unsatisfied dependency for type org.kie.kogito.event.EventEmitter and qualifiers [@Default]
        - java member: com.jongunter.TestMessageProducer_1#emitter
        - declared on CLASS bean [types=[com.jongunter.TestMessageProducer_1, org.kie.kogito.services.event.impl.AbstractMessageProducer<java.lang.String, com.jongunter.TestMessageDataEvent_1>, java.lang.Object], qualifiers=[@Default, @Any], target=com.jongunter.TestMessageProducer_1]
        The following beans match by type, but none have matching qualifiers:
                - Bean [class=org.kie.kogito.app.HelloworldEventEmitter, qualifiers=[@HelloworldQualifier, @Any]]
        at io.quarkus.arc.processor.Beans.resolveInjectionPoint(Beans.java:428)
        at io.quarkus.arc.processor.BeanInfo.init(BeanInfo.java:524)
        at io.quarkus.arc.processor.BeanDeployment.init(BeanDeployment.java:260)
        ... 13 more

        at io.quarkus.runner.bootstrap.AugmentActionImpl.runAugment(AugmentActionImpl.java:330)
        at io.quarkus.runner.bootstrap.AugmentActionImpl.createInitialRuntimeApplication(AugmentActionImpl.java:252)
        at io.quarkus.runner.bootstrap.AugmentActionImpl.createInitialRuntimeApplication(AugmentActionImpl.java:60)
        at io.quarkus.deployment.dev.IsolatedDevModeMain.firstStart(IsolatedDevModeMain.java:92)
        at io.quarkus.deployment.dev.IsolatedDevModeMain.accept(IsolatedDevModeMain.java:455)
        at io.quarkus.deployment.dev.IsolatedDevModeMain.accept(IsolatedDevModeMain.java:66)
        at io.quarkus.bootstrap.app.CuratedApplication.runInCl(CuratedApplication.java:140)
        at io.quarkus.bootstrap.app.CuratedApplication.runInAugmentClassLoader(CuratedApplication.java:96)
        at io.quarkus.deployment.dev.DevModeMain.start(DevModeMain.java:132)
        at io.quarkus.deployment.dev.DevModeMain.main(DevModeMain.java:62)
Caused by: io.quarkus.builder.BuildException: Build failure: Build failed due to errors
        [error]: Build step io.quarkus.arc.deployment.ArcProcessor#validate threw an exception: javax.enterprise.inject.spi.DeploymentException: javax.enterprise.inject.UnsatisfiedResolutionException: Unsatisfied dependency for type org.kie.kogito.event.EventEmitter and qualifiers [@Default]
        - java member: com.jongunter.TestMessageProducer_1#emitter
        - declared on CLASS bean [types=[com.jongunter.TestMessageProducer_1, org.kie.kogito.services.event.impl.AbstractMessageProducer<java.lang.String, com.jongunter.TestMessageDataEvent_1>, java.lang.Object], qualifiers=[@Default, @Any], target=com.jongunter.TestMessageProducer_1]
        The following beans match by type, but none have matching qualifiers:
                - Bean [class=org.kie.kogito.app.HelloworldEventEmitter, qualifiers=[@HelloworldQualifier, @Any]]
        at io.quarkus.arc.processor.BeanDeployment.processErrors(BeanDeployment.java:1202)
        at io.quarkus.arc.processor.BeanDeployment.init(BeanDeployment.java:272)
        at io.quarkus.arc.processor.BeanProcessor.initialize(BeanProcessor.java:134)
        at io.quarkus.arc.deployment.ArcProcessor.validate(ArcProcessor.java:462)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:77)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.base/java.lang.reflect.Method.invoke(Method.java:568)
        at io.quarkus.deployment.ExtensionLoader$2.execute(ExtensionLoader.java:882)
        at io.quarkus.builder.BuildContext.run(BuildContext.java:277)
        at org.jboss.threads.ContextHandler$1.runWith(ContextHandler.java:18)
        at org.jboss.threads.EnhancedQueueExecutor$Task.run(EnhancedQueueExecutor.java:2449)
        at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.run(EnhancedQueueExecutor.java:1478)
        at java.base/java.lang.Thread.run(Thread.java:833)
        at org.jboss.threads.JBossThread.run(JBossThread.java:501)
Caused by: javax.enterprise.inject.UnsatisfiedResolutionException: Unsatisfied dependency for type org.kie.kogito.event.EventEmitter and qualifiers [@Default]
        - java member: com.jongunter.TestMessageProducer_1#emitter
        - declared on CLASS bean [types=[com.jongunter.TestMessageProducer_1, org.kie.kogito.services.event.impl.AbstractMessageProducer<java.lang.String, com.jongunter.TestMessageDataEvent_1>, java.lang.Object], qualifiers=[@Default, @Any], target=com.jongunter.TestMessageProducer_1]
        The following beans match by type, but none have matching qualifiers:
                - Bean [class=org.kie.kogito.app.HelloworldEventEmitter, qualifiers=[@HelloworldQualifier, @Any]]
        at io.quarkus.arc.processor.Beans.resolveInjectionPoint(Beans.java:428)
        at io.quarkus.arc.processor.BeanInfo.init(BeanInfo.java:524)
        at io.quarkus.arc.processor.BeanDeployment.init(BeanDeployment.java:260)
        ... 13 more

        at io.quarkus.builder.Execution.run(Execution.java:116)
        at io.quarkus.builder.BuildExecutionBuilder.execute(BuildExecutionBuilder.java:79)
        at io.quarkus.deployment.QuarkusAugmentor.run(QuarkusAugmentor.java:157)
        at io.quarkus.runner.bootstrap.AugmentActionImpl.runAugment(AugmentActionImpl.java:328)
        ... 9 more
Caused by: javax.enterprise.inject.spi.DeploymentException: javax.enterprise.inject.UnsatisfiedResolutionException: Unsatisfied dependency for type org.kie.kogito.event.EventEmitter and qualifiers [@Default]
        - java member: com.jongunter.TestMessageProducer_1#emitter
        - declared on CLASS bean [types=[com.jongunter.TestMessageProducer_1, org.kie.kogito.services.event.impl.AbstractMessageProducer<java.lang.String, com.jongunter.TestMessageDataEvent_1>, java.lang.Object], qualifiers=[@Default, @Any], target=com.jongunter.TestMessageProducer_1]
        The following beans match by type, but none have matching qualifiers:
                - Bean [class=org.kie.kogito.app.HelloworldEventEmitter, qualifiers=[@HelloworldQualifier, @Any]]
        at io.quarkus.arc.processor.BeanDeployment.processErrors(BeanDeployment.java:1202)
        at io.quarkusocessor.BeanDeployment.init(BeanDeployment.java:272)
        at io.quarkus.arc.processor.BeanProcessor.initialize(BeanProcessor.java:134)
        at io.quarkus.arc.deployment.ArcProcessor.validate(ArcProcessor.java:462)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:77)
        at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.base/java.lang.reflect.Method.invoke(Method.java:568)
        at io.quarkus.deployment.ExtensionLoader$2.execute(ExtensionLoader.java:882)
        at io.quarkus.builder.BuildContext.run(BuildContext.java:277)
        at org.jboss.threads.ContextHandler$1.runWith(ContextHandler.java:18)
        at org.jboss.threads.EnhancedQueueExecutor$Task.run(EnhancedQueueExecutor.java:2449)
        at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.run(EnhancedQueueExecutor.java:1478)
        at java.base/java.lang.Thread.run(Thread.java:833)
        at org.jboss.threads.JBossThread.run(JBossThread.java:501)
Caused by: javax.enterprise.inject.UnsatisfiedResolutionException: Unsatisfied dependency for type org.kie.kogito.event.EventEmitter and qualifiers [@Default]
        - java member: com.jongunter.TestMessageProducer_1#emitter
        - declared on CLASS bean [types=[com.jongunter.TestMessageProducer_1, org.kie.kogito.services.event.impl.AbstractMessageProducer<java.lang.String, com.jongunter.TestMessageDataEvent_1>, java.lang.Object], qualifiers=[@Default, @Any], target=com.jongunter.TestMessageProducer_1]
        The following beans match by type, but none have matching qualifiers:
                - Bean [class=org.kie.kogito.app.HelloworldEventEmitter, qualifiers=[@HelloworldQualifier, @Any]]
        at io.quarkus.arc.processor.Beans.resolveInjectionPoint(Beans.java:428)
        at io.quarkus.arc.processor.BeanInfo.init(BeanInfo.java:524)
        at io.quarkus.arc.processor.BeanDeployment.init(BeanDeployment.java:260)
        ... 13 more

```

## Branches
- `main` - broken example with 2 `hello-world` message nodes 
- `working` - working process just 1 `hello-world` message node

## Running the application

Run (ensure you have Kafka running locally at `localhost:9092`)
```shell script
./mvnw compile quarkus:dev
```

Kick off my little test process
```shell
curl --location --request POST 'http://localhost:8080/test' \
--header 'Content-Type: application/json' \
--data-raw '{
	"message": "foobar"
}'
```
