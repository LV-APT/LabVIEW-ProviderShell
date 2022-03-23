# LabVIEW-ProviderShell

支持 LabVIEW Provider 机制的实现。

## 1 Class Provider: LabVIEW-ClassProviderShell

This library implements a plugin mechanism for LabVIEW Class. It loads LabVIEW classes from a disk path and converts them to the parent class.

### 1.1 API

#### 1.1.1 Key API

* **`LoadLvClasses.vim`** loads LabVIEW class from a disk path and converts them to the parent class. 
    * `Path` specifies the absolute path to the classes to load. **Note**: Folders that start with `_` or `.` will be ignored.
    * `ClassType` specifies the target class type to load. Those classes that are children of the `ClassType` will be loaded, and the returned classes will be converted to `ClassType`.
    * `milliseconds to wait` specifies the time, in milliseconds, that the function waits for loading the classes. The default is -1, indicating to wait until done.
    * `error in` describes error conditions that occur before this node runs.
    * `Loaded Classes` returns the loaded classes.
    * `error out` contains error information.

![image](https://user-images.githubusercontent.com/64485819/159438054-01573c31-d9a3-4a3b-a03d-90ee7da41d6e.png)

#### 1.1.2 Utilities

The following utilities provide tools to obtain corresponding LabVIEW class information.

* `Get LV Class ParentName.vim`
* `Get LV Class Version.vim`
* `Get LV Class Hierarchy.vim`
* `Get LV Class Description.vim`

![image](https://user-images.githubusercontent.com/64485819/159635100-98c5ceac-2c04-4942-b827-c5c0d181764a.png)


### 1.2 Example

The `Calculator Example` provided by the library demonstrates the plugin mechanism of LabVIEW Class Provider. The math functions of this calculator are loaded dynamically as plugins. Therefore, the calculator has very good scalability.

<!-- ![image](https://user-images.githubusercontent.com/64485819/159439155-47f6217d-8029-4847-8ed7-6d0259d904ce.png)
![image](https://user-images.githubusercontent.com/64485819/159439496-a805673a-b5d7-4c62-b3b8-7306c0355f76.png) -->

![image](https://user-images.githubusercontent.com/64485819/159602963-c6e8e4c4-1e1e-4649-9d69-7c799031f52c.png)

### 1.3 Distribution Consideration

This library supports the following forms of code distribution,

1. The shell class is distributed as source code (`*.lvclass`, `*.llb`).
2. The shell class is distributed as a packed library (`*.lvlibp`).

In both situations, the plugin classes can be distributed as source code, packed library, or a mix of both. Notice that the plugin classes must inherit the shell class, whether as source code or as a packed library. In the usual situation, the shell class is often distributed as a packed library (`*.lvlibp`), so that the shell functions are fixed and uncontaminated. And after the shell is released the plugins can be freely designed by different developers.

------



## 2 VI Provider: LabVIEW-VIProviderShell

### Steps

1. 创建实际执行的VI (provider Content VIs), 它们有相同的Connect Pane;
2. 创建 Provider VI, 和实际执行的VI (provider Content VIs)具有相同的 Connect Pane;
3. 拷贝 Template，将所有接线端子放在 Disable Structure 中；
4. *调用方通过 PrepareProviderCall.vi 修改 Provider 实际执行的 VI 路径。

### Dependencies
- OpenG Data Library
- OpenG String Library
- OpenG File Library
- OpenG Application Library
- OpenG Error Library
