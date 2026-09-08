# 桌宠模板增强

这仍然是生成独立 Windows/Python 桌宠的 skill，不是 Codex 原生 Custom pets 导入器。

- 所有新生成的项目继承增量事件监听、动作联动和字幕设置，而非仅限于“遥”。
- 启动 / 完成 / 中断分别对应移动循环 / 互动一次 / 坐下。设置中可关闭动作联动。
- 后台线程每 250ms 轮询新增日志，处理半行写入、坏行、文件缩短及不同回合事件。不再以日志8秒未修改来判定待机。
- 字幕只显示状态，中英文切换、水平垂直居中、透明背景，窄幅可换行。
- 设置中可指定跟踪任务ID；留空时启动选最新日志并固定跟踪，避免多个任务相互干扰。不会自动跟随当前打开的Codex页面。
- 退出/崩溃若没有写入终止事件，单靠日志不能确认结束。远程任务或ChatGPT任务没有本地rollout时不能同步。
- 原有全屏自动隐藏逻辑未重写，默认关闭；可自行开启。
- 新增“遥”默认时装的五种动画，共850帧，并保留原有予愿安洁莉娜。

## 使用

`python ark-codex-skill/scripts/scaffold_deskpet.py --target my-pet --pet 遥`

`python ark-codex-skill/scripts/setup_env.py my-pet`

然后运行 `my-pet/启动桌宠.bat`。生成目标须为空，已有项目升级请先备份并合并程序文件，不覆盖settings.json或.venv。

Python 3.14在本地完成了UI与事件测试。环境安装失败应按实际权限、网络或依赖报错处理，不自动删除虚拟环境，也不因此推断Python版本不兼容。

## 验证

在装有PySide6的Python中运行 `python -m unittest discover -s tests -v`。

此Fork中的模板是生成项目的来源。独立软件仓库从模板同步，不在两边分别实现相同功能。导出与抽帧脚本留在skill仓库。
