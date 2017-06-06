# 安装

    pip install fis3
    
# 替换原来的render_template渲染

    app = Flask(__name__)
    FIS(app, static_folder="static", template_folder="templates")
    
    @app.route('/')
    def index():
        return FIS.render_template('page/index/index.html', title='index')
        
# 使用蓝图时要带上命名空间

    www = Blueprint('www', __name__)
    
    @www.route('/')
    def index():
        return FIS.render_template('www:page/index/index.html', title='index')

# 扩展jinja2

    [参考fis3官方推荐语法](https://github.com/fex-team/fis3-solutions/blob/master/spec.md#语法糖扩展)

    {% fis_framework 'static/lib/mod.js' %}
    
    {% fis_placeholder 'css' %} 
    {% fis_placeholder 'framework' %}
    {% fis_placeholder 'resource_map' %}
    {% fis_placeholder 'js' %}
    
    {% fis_load 'widget/a/a.css' %}
    
    {% fis_uri 'page/demo/demo.html' %}
    
    {% fis_style %}
        <style>
            body{
                color: red;
            }
        </style>
    {% end_fis_style %}
    
    {% fis_script %}
        <script>
            require('./demo')
        </script>
    {% end_fis_script %}
    
    //继承和导入采用原来的语法
    {% extends 'page/template.html' %}
    {% include 'widget/green/green.html' %}
    
# 一个经典的母模板

    <!DOCTYPE html>
    <html>
    <head>
        <meta charset="UTF-8">
        <title>{{ title if title }}</title>
        {% block head %}{% endblock %}
        {% fis_framework 'static/lib/mod.js' %}
        {% fis_placeholder 'css' %}
    </head>
    <body>
    {% block body %}{% endblock %}
    {% block script %}
        {% fis_placeholder 'framework' %}
        {% fis_placeholder 'resource_map' %}
        {% fis_placeholder 'js' %}
    {% endblock %}
    </body>
    </html>
    

        
# 发布到pypi

    python setup.py sdist
    python setup.py register -r pypi  #只要注册一次
    python setup.py sdist upload -r pypi