# 发布到pypi

    python setup.py sdist
    python setup.py register -r pypi  #只要注册一次
    python setup.py sdist upload -r pypi