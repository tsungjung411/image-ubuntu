# Usages:
#   # build the image (take 9 minutes)
#   $ docker build -t ubuntu18.04-python3.8 .

FROM ubuntu:18.04


# [Software Repository]
#
# update the Ubuntu software repository 
#
# - for the 'tzdata' package, or you will meet:
#   E: Unable to locate package tzdata
#
# - for the 'software-properties-common' package, or you will meet:
#   E: Unable to locate package software-properties-common
#
RUN apt update \
    && apt install -y curl wget


# [Timezone]
#
# Avoiding user interaction with tzdata when installing some packages, 
# e.g. 'software-properties-common', 'python3-sklearn', 'parabricks.deb'
#
# i.e. some packages may ask for your timezone, and block the 
# installation process.
# -------------------------------------------------------------------
# log:
#
#   Configuring tzdata
#   ------------------
#   Please select the geographic area in which you live. Subsequent 
#   configuration questions will narrow this down by presenting a 
#   list of cities, representing the time zones in which they are 
#   located.
# 
#     1. Africa        6. Asia            11. System V timezones
#     2. America       7. Atlantic Ocean  12. US
#     3. Antarctica    8. Europe          13. None of the above
#     4. Australia     9. Indian Ocean
#     5. Arctic Ocean  10. Pacific Ocean
# 
# solutions:
#  - https://askubuntu.com/questions/909277/
#    `ENV DEBIAN_FRONTEND=noninteractive` for `apt install tzdata`
#  - https://cynthiachuang.github.io/Change-Timezone-in-Dockerfile/
#  - https://ubuntuqa.com/zh-tw/article/7684.html
#
ENV DEBIAN_FRONTEND=noninteractive
RUN apt install tzdata \
    && TZ=Asia/Taipei \
	&& ln -snf /usr/share/zoneinfo/$TZ /etc/localtime \
	&& echo $TZ > /etc/timezone \
	&& dpkg-reconfigure -f noninteractive tzdata


# ENV LANG=C.UTF-8


# [Python3]
#
# install Python 3.5 / 3.6 / 3.7 / 3.8 / 3.9 / 3.10
# https://www.python.org/downloads/

# prepare for 'add-apt-repository'
# - for 'add-apt-repository' command, or you will meet:
#   bash: add-apt-repository: command not found
#
# - currently, the command below will also install python 3.6 for Ubuntu 18.04 by default
#   Python 3.6.9 (default, 2022/08/17, 16:25)
#
RUN apt install -y software-properties-common

# install Python3.8
# - version: Python 3.8.0 (default, Dec  9 2021, 17:53:27)
RUN apt install -y python3.8 python3-pip

# create shortcuts & upgrade pip (9.0.1 -> 22.2.2)
RUN ln -sf /usr/bin/python3.8 /usr/bin/python3 \
    && ln -s /usr/bin/python3.8 /usr/bin/python \
    && python --version \
    && python3 --version \
    && python3.8 --version \
    \
    && ln -s /usr/bin/pip3 /usr/bin/pip \
    && pip --version \
    && pip3 --version \
    \
    && python3.8 -m pip install --upgrade --force-reinstall pip \
    && pip --version \
    && pip3 --version


