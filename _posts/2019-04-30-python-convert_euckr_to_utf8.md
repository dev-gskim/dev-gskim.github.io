## EUC-KR 파일을 UTF-8 파일로 변경

* 인자값은 파일명
* 사용법 

~~~ python
import os
import sys
import codecs

#######################################################
# usage   : python euckr_to_utf8.py {file name}
# example : python euckr_to_utf8.py test1.csv
# result  : create test1-UTF8.csv
#######################################################

# check file exists
def chk_exists_file(file_name):
    return os.path.exists(file_name)

# transform euc-kr to utf-8
def conv_euckr_to_utf8(file_name):
    # for utf-8 file name
    file_nm = os.path.splitext(file_name)[0]
    file_ext = os.path.splitext(file_name)[1]
    file_name_utf8 = file_nm + '-UTF8' + file_ext
    print (file_name_utf8)

    # euc-kr to utf-8
    print ('transform incoding ...')
    file_src = codecs.open(file_name, 'r', encoding='euc-kr')
    file_utf8 = codecs.open(file_name_utf8, 'w', encoding='utf-8')

    s = file_src.read()
    file_utf8.write(s)
    
    file_src.close()
    file_utf8.close()
    print ('transform complete')

if __name__ == "__main__":
    if len(sys.argv) <= 1:
        print('please file name')
    else:
        print('file name : [%s]' % sys.argv[1])
        if chk_exists_file(sys.argv[1]):
            conv_euckr_to_utf8(sys.argv[1])
        else:
            print('file not exists')
~~~
