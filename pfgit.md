#! /usr/bin/python
# -* - coding: UTF-8 -* -
import ConfigParser
import os
import os.path
import sys
import getopt

# 所有module的分支名
module_branch = []
# 所有module的远程地址
branch_url = []
# 所有module的文件名
name_list = []

config_name = "config.cfg"

config = ConfigParser.ConfigParser();
config.read(config_name)
sections = config.sections()
for i in range(len(sections)):
    options = config.options(sections[i])
    if len(options) > 2:
        str_url = config.get(sections[i], options[0])
        str_name = config.get(sections[i], options[1])
        str_branch = config.get(sections[i], options[2])
        name_list.insert(i, str_name)
        branch_url.insert(i, str_url)
        module_branch.insert(i, str_branch)


# 获取当前路径
root_dir = os.path.abspath(os.curdir)



def usage():
    print '''
    python sys.srgv[0] [options] [values]...
    [optins]
    --help
    -p, --pull
    -P, --push
    -c, --checkout
    --path
    '''



# 批量切分支
def checkoutBranch():
  for i in range(len(name_list)):

    cur_path = root_dir + '/' + name_list[i]

    # 切换到项目路径
    os.chdir(cur_path)

    # 执行切换环境
    print 'git checkout ' + str(name_list[i])
    os.system('git checkout ' + module_branch[i])

def chekoutParamsBranch(branch):
    for i in range(len(name_list)):

        cur_path = root_dir + '/' + name_list[i]

        # 切换到项目路径
        os.chdir(cur_path)

        # 执行切换环境
        print 'git checkout ' + branch
        os.system('git checkout ' + branch)


# 批量从远程拉去分支
def pullFromRemote():
  for i in range(len(name_list)):

    cur_path = root_dir + '/' + name_list[i]

    # 切换到项目路径
    os.chdir(cur_path)

    # 执行切换环境
    os.system('git checkout origin/' + module_branch[i] + " -b " + module_branch[i])
    print 'git checkout origin/' + str(module_branch[i]) + " -b " + str(name_list[i])



# 批量推送到远程仓库
def pushToRemote(param):
  for i in range(len(name_list)):

    cur_path = root_dir + '/' + name_list[i]

    # 切换到项目路径
    os.chdir(cur_path)

    # 执行切换环境
    if name_list[i] != 'LoginModule' and name_list[i] != 'TDFMessageModule':
       # os.system('git checkout -b feature/home_data_change')
       os.system('git push --set-upstream origin ' + param)



# 批量拉取
def pull():
  for i in range(len(name_list)):

    cur_path = root_dir + '/' + name_list[i]

    # 切换到项目路径
    os.chdir(cur_path)

    # 执行切换环境
    print 'git pull ' + str(name_list[i])
    os.system('git pull')



# 批量提交
  def pull():
    for i in range(len(name_list)):

      cur_path = root_dir + '/' + name_list[i]

      # 切换到项目路径
      os.chdir(cur_path)

      # 执行切换环境
      os.system('git push')
      print 'git push ' + str(name_list[i])



def main():
    shortargs = 'hpPc'
    longargs = ["help", "pull", "push", "checkout=", "path="]

    try:
        opts, args = getopt.getopt(sys.argv[1:], shortargs, longargs)
    except getopt.GetoptError:
        usage()
        sys.exit(1)
    for a, o in opts:
        if a in ("-h", "--help"):
            usage()
        elif a in ("-p", "--pull"):
            pull()
        elif a in ("-P", "--push"):
            push()
        elif a in ("-c", "--checkout"):
            if len(o) > 0:
                chekoutParamsBranch(o)
            else:
                checkoutBranch()
        elif a == "--path":
            config_name = o



if __name__ == "__main__":
    if len(sys.argv) == 1:
        usage()
        sys.exit(1)
    else:
        main()