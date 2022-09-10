### CourtCanva

github 用 `.` + `enter` 可以打开云 VScode。

接收新项目，看readme中代码守则。

之后看 package.json 中的 scripts。 lint 与 eslint 是代码规范，prettier 代码美化。 coverage 是代码测试覆盖量。cypress也是测试，不同方向。e2e也是测试（也要写）。prepare 是 husky（commit 时候的检查）。

public 是所有静态资源。

测试：unit test /integration test /e2e test  小/中/大  一个api就是一个小的 unit

postman 属于外层测试，中/大型的。因为用的mock data，所以不会对数据库造成影响。



后端 要更新 migrate-up: migrate-mongo up 功能

连 mongodb compass