# LabVIEW-ProviderShell

支持 LabVIEW Provider 机制的实现。

![Tempate](Documentation\main.png)

Steps:

1. 创建实际执行的VI (provider Content VIs), 它们有相同的Connect Pane;
2. 创建 Provider VI, 和实际执行的VI (provider Content VIs)具有相同的 Connect Pane;
3. 拷贝 Template，将所有接线端子放在 Disable Structure 中；
4. *调用方通过 PrepareProviderCall.vi 修改 Provider 实际执行的 VI 路径。

### 依赖

- NEVSTOP-Programming-Palette
- OpenG Data Library
- OpenG String Library
- OpenG Path Library
- OpenG Application Library
- OpenG Error Library
