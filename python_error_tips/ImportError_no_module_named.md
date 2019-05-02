## " ImportError: no module named ' ' " 



1. 빈 파일이라도 불러오려는 모듈(파이썬 파일)이 있는 폴더에 ![1556780785691](C:\Users\seoyein\AppData\Roaming\Typora\typora-user-images\1556780785691.png)를 만든다. [링크] https://stackoverflow.com/questions/338768/python-error-importerror-no-module-named
2. 그래도 안 되면 os.chdir()로 해당 모듈이 있는 폴더로 경로를 변경하는 코드를 추가한다.
3. 그래도 안 되면 sys.path.append()를 이용해 모듈이 있는 경로를 추가한다. 
4. 커널에서 돌릴 경우 python3라고 지정을 해 준다(python2로 돌아가는 경우가 있다고..) [링크] <https://github.com/FinanceData/FinanceDataReader/issues/14>

