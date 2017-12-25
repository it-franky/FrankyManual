
* 电子书：[Sublime_Text_Power_User](E:\Baidu Netdisk\Ebook&Document\Tools\Sublime_Text_Power_User.pdf)

#### Sublime text 3

<table>
    <tr>
        <td>快捷键</td>
        <td>描述</td>
    </tr>
    <tr>
        <td>cdhm</td>
        <td>192.168.137.117</td>
    </tr>
    <tr>
        <td>cdhs1</td>
        <td>192.168.137.119</td>
    </tr>
    <tr>
        <td>cdhs2</td>
        <td>192.168.137.120</td>
    </tr>
</table>



#### 创建一个项目

>Project->Add Folder to Project……


#### 配置预览快捷键

```javascript
Preferences —< Key Bindings - User 将以下代码复制到数组中。
// chrome
{ "keys": ["f2"], "command": "side_bar_files_open_with",        
       "args": {            
            "paths": [],            
            "application": "C:/Program Files (x86)/Google/Chrome/Application/chrome.exe",            
            "extensions":".*"        
        }
 },
// firefox
{ "keys": ["f3"], "command": "side_bar_files_open_with",         
        "args": {            
            "paths": [],            
            "application": "D:/Program Files (x86)/Mozilla Firefox/firefox.exe",                
            "extensions":".*"        
            }
},
// ie 
{ "keys": ["f4"], "command": "side_bar_files_open_with",         
            "args": {            
            "paths": [],            
            "application": "C:/Program Files/Internet Explorer/iexplore.exe",                     
            "extensions":".*"        
            }
}
```
### Package Control

插件管理器，可以使用众多的插件来扩展Sublime的功能。

#### INSTALLATION
The simplest method of installation is through the Sublime Text console. The console is accessed via the ctrl+` shortcut or the View > Show Console menu. Once open, paste the appropriate Python code for your version of Sublime Text into the console.

```python
import urllib.request,os,hashlib; h = 'df21e130d211cfc94d9b0905775a7c0f' + '1e3d39e33b79698005270310898eea76'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
```

#### Sidebar Enhancements

Provides enhancements to the operations on Sidebar of Files and Folders for Sublime Text. 

#### Markdown Extended

Markdown syntax highlighter for Sublime Text, with extended support for GFM fenced code blocks, with language-specific syntax highlighting. YAML Front Matter. Works with ST2/ST3. Goes great with Assemble.

#### Markdown Preview

markdown preview and build plugin for sublime text 2/3

#### Anaconda

Anaconda turns your Sublime Text 3 in a full featured Python development IDE

#### Djaneiro

Django support for Sublime Text 2/3

#### Emmet
Emmet is a plugin for many popular text editors which greatly improves HTML & CSS workflow

* Expand Abbreviation – Tab or Ctrl+E

#### Python PEP8 Autoformat

Python PEP8 Autoformat is a Sublime Text plugin to interactively reformat Python source code according to PEP-8 (Style Guide for Python Code). 

Using keyboard:

* GNU/Linux: ctrl+shift+r
* OSX: ctrl+shift+r
* Windows: ctrl+shift+r

#### Advanced​New​File

Advanced file creation for Sublime Text 2 and Sublime Text 3.

<table>
    <tr>
        <td>快捷键</td>
        <td>描述</td>
    </tr>
    <tr>
        <td>ctrl+alt+n</td>
        <td>General keymap to create new files.</td>
    </tr>
    <tr>
</table>

#### HTMLBeautify

A plugin for Sublime Text that formats (indents) HTML source code. It makes code easier for humans to read.

<table>
    <tr>
        <td>快捷键</td>
        <td>描述</td>
    </tr>
    <tr>
        <td>Control-Alt-Shift-F</td>
        <td>formats (indents) HTML source code.</td>
    </tr>
    <tr>
</table>


#### Delete​Blank​Lines

Deletes blank (or surplus blank) lines from a selection

<table>
    <tr>
        <td>快捷键</td>
        <td>描述</td>
    </tr>
    <tr>
        <td>Ctrl+Alt+Backspace</td>
        <td>Delete Blank Lines</td>
    </tr>
    <tr>
</table>

#### Nettuts+ Fetch

Fetch the latest version of remote files and zip packages.



#### Doc​Blockr

Simplifies writing DocBlock comments in Javascript, PHP, CoffeeScript, Actionscript, C & C++

#### JSHint

The best JavaScript syntax checker: JSHint for the best text editor: Sublime Text

