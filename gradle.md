####  检查依赖报告

运行命令./gradlew <projectname>:dependencies --configuration compile （projectname为settings.gradle里面配置的各个project，
如果没有配置，直接运行./gradlew dependencies --configuration compile），
会把依赖树会打印出来，依赖树显示了你 build 脚本声明的顶级依赖和它们的传递依赖： 