# Code Optimizer for C programs
Using pycparser to accomplish replacement of sensitive snippets to more healthy ones.<br>

完成敏感代码片段的替换以获得质量更高的代码

## Explaination
This extension is made for **vscode** . The extension uses the power of **pycparser** to generate an *AST* of C file in an active editor window.<br>

The C file may possibly contain harmful snippets which cause buffer overflow （导致缓冲区溢出的有害代码段） and these may write to sensitive blocks of memory.<br>
To avoid that we replace those snippets of code with their better halfs.<br>

## Requirements
- [pycparser](https://github.com/eliben/pycparser)
- [python shell](https://github.com/extrabacon/python-shell)
- shelljs
- node.js.
- vscode *(OFCOURSE)*

## Installation
- Clone the Repo and install the requirements first.
- Put the whole folder to the following path:
    - Linux / Mac : _$HOME/.vscode/extensions_
    - Windows : _%USERPROFILE%\.vscode\extensions_
- You're done. The extension has been setup.

## Extending the database
Currently we have few snippets of code that we are replacing. But it can be extended by the following steps:
 - In _req/doASTcheck/checkAST.py_  按敏感模式匹配 扫描源代码 发现 敏感代码片段:
 	- update the classMap dictionary with the classes as key that maybe involved in buffer overflow and their start and end lines in _req/doASTcheck/initialPattern.txt_ file. 
 		~~~~
 		Example : classMap = {'FuncCall':(1,10)}
 		~~~~
 - In _req/doASTcheck/initialPattern.txt_   敏感的代码片段模式 :
 	- update the patterns you want to find in the file in the following format. ( In the below code replace_lines refer to those in _req/doASTreplace/replacementPattern.txt_ file).
 		~~~~
 		start: line_with_which_to_replace_start : line_with_which_to_replace_end
 			// the pattern
 		end:
 		~~~~
 - In _req/doASTreplace/replacementPattern.txt_  建议替换为的模式 :
 	-  update the patterns that is to be replaced in the following format.
 		~~~~
 		//the pattern
 		~~~~
 - In _req/doASTreplace/replaceAST.py_  根据匹配模式 修改 敏感代码片段的 AST树
 
## Tests
We have checked the plugin on Ubuntu 15.04 and 16.04. It is yet to be tested on Windows.
Further some classes ( in checkAST.py ) have not been fully coded as we did not see any harmful snippets produced by those. So as we discover more such threats, we'll update the code.
