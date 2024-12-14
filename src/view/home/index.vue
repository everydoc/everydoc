<template>
  <div>
    <div ref="echartsContainer" style="width: 100%; height: 1400px"></div>
  </div>
</template>
  
  <script>
import { onMounted, reactive, ref } from "vue";
import * as echarts from "echarts";

export default {
  name: "KnowledgeGraph",
  setup() {
    // 使用 ref 获取 DOM 容器
    const echartsContainer = ref(null);

    // 初始化 ECharts 图表
    const initECharts = () => {
      const myChart = echarts.init(echartsContainer.value);
      function uniqueBy(dataSet, field) {
        let dest = [];
        for (let i = 0; i < dataSet.length; i++) {
            let ai = dataSet[i];
            if (i === 0) {
                dest.push(ai);
            } else {
                let filterData = dest.filter(function (e) {
                    return e[field] === ai[field];
                })
                if (filterData.length === 0) {
                    dest.push(ai);
                }
            }
        }
        return dest;
    }
      // 配置图表的选项
      const option = {
        title: {
          x: 0,
          y: 37,
          text: "知识图谱",
          subtext:
            "单击文章节点跳转至指定文章页面，双击标签/分类，展示指定标签/分类的图谱信息",
        },
        tooltip: { show: false },
        legend: {
          orient: "vertical",
          x: 70,
          y: "center",
          // selected: {'文章': false},
          data: getGraph().categories.map(function (c) {
            return c.name;
          }),
        },
        animationDuration: 1500,
        animationEasingUpdate: "quinticInOut",
        series: [
          {
            name: "知识图谱",
            type: "graph",
            layout: "force",
            force: {
              repulsion: 1,
              edgeLength: 7,
            },
            data: getGraph().nodes,
            links: getGraph().links,
            categories: getGraph().categories,
            roam: false, // 缩放
            draggable: true,
            label: {
              position: "right",
              formatter: "{b}",
            },
            edgeSymbol: ["none", "arrow"],
            lineStyle: {
              color: "source",
              curveness: 0.01,
            },
            emphasis: {
              focus: "adjacency",
              lineStyle: {
                width: 3,
              },
            },
          },
        ],
      };
      function randomX() {
        return Math.random() * 38.2
    }    function randomY() {
        return Math.random() * 61.8
    }
      function getGraph(){
        let categories = [
            {"name": "分类"},
            {"name": "标签"},
            {"name": "文章"}
        ];

        let nodes_post = [{
                    "id": "/tools/2021/12/05/ddns.html",
                    "name": "ddns",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/tools/2021/12/05/ddns.html"
                },{
                    "id": "/tools/2021/12/03/nacos.html",
                    "name": "nacos",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/tools/2021/12/03/nacos.html"
                },{
                    "id": "/tools/2021/12/01/docsify.html",
                    "name": "docsify打包docker镜像",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/tools/2021/12/01/docsify.html"
                },{
                    "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/11/17/es.html",
                    "name": "ES数据操作",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/11/17/es.html"
                },{
                    "id": "/%E5%B7%A5%E5%85%B7/2020/06/17/sublime.html",
                    "name": "Sublime 快捷键",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%B7%A5%E5%85%B7/2020/06/17/sublime.html"
                },{
                    "id": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2020/06/01/ddp.html",
                    "name": "设计模式-访问者模式",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2020/06/01/ddp.html"
                },{
                    "id": "/linux/2020/05/06/test-all-in-one.html",
                    "name": "测试工具使用",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/linux/2020/05/06/test-all-in-one.html"
                },{
                    "id": "/linux/2020/05/06/arthas.html",
                    "name": "Arthas使用教程",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/linux/2020/05/06/arthas.html"
                },{
                    "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/19/ssh.html",
                    "name": "SSH免密登录",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/19/ssh.html"
                },{
                    "id": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/04/19/eggplant.html",
                    "name": "风味茄子",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/04/19/eggplant.html"
                },{
                    "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/04/12/hadoop.html",
                    "name": "Hadoop 搭建",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/04/12/hadoop.html"
                },{
                    "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/11/ci.html",
                    "name": "Jenkins 环境搭建",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/11/ci.html"
                },{
                    "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/03/apm.html",
                    "name": "APM搭建使用",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/03/apm.html"
                },{
                    "id": "/personal/2020/03/07/the-art-of-talk.html",
                    "name": "说话的艺术",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/personal/2020/03/07/the-art-of-talk.html"
                },{
                    "id": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/02/17/Once-Upon-a-Time-in-Hollywood.html",
                    "name": "好莱坞往事",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/02/17/Once-Upon-a-Time-in-Hollywood.html"
                },{
                    "id": "/personal/2020/02/16/fire.html",
                    "name": "FIRE",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/personal/2020/02/16/fire.html"
                },{
                    "id": "/inmgr/2020/02/14/the-future-of-inmgr.html",
                    "name": "接口平台的反思与发展",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/inmgr/2020/02/14/the-future-of-inmgr.html"
                },{
                    "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/21/Flink-All-in-one.html",
                    "name": "Flink All in one",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/21/Flink-All-in-one.html"
                },{
                    "id": "/tools/2020/01/20/tesseract.html",
                    "name": "Tesseract 使用记录",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/tools/2020/01/20/tesseract.html"
                },{
                    "id": "/%E4%BB%A3%E7%A0%81/2020/01/19/git.html",
                    "name": "Git 操作使用",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E4%BB%A3%E7%A0%81/2020/01/19/git.html"
                },{
                    "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/19/efk.html",
                    "name": "EFK 搭建使用",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/19/efk.html"
                },{
                    "id": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2020/01/17/static-pages-based-on-jekyll.html",
                    "name": "Jekyll静态博客",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2020/01/17/static-pages-based-on-jekyll.html"
                },{
                    "id": "/java/2020/01/12/jvm.html",
                    "name": "Java All in One",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/java/2020/01/12/jvm.html"
                },{
                    "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/01/02/maven.html",
                    "name": "Maven All in One",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/01/02/maven.html"
                },{
                    "id": "/db/2020/01/01/redis.html",
                    "name": "redis",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/db/2020/01/01/redis.html"
                },{
                    "id": "/db/2020/01/01/mongodb.html",
                    "name": "MongoDB",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/db/2020/01/01/mongodb.html"
                },{
                    "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2019/12/31/jrebel-license-server.html",
                    "name": "Jrebel激活服务",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2019/12/31/jrebel-license-server.html"
                },{
                    "id": "/%E4%BB%A3%E7%A0%81/2019/12/21/json.html",
                    "name": "Json All in One",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E4%BB%A3%E7%A0%81/2019/12/21/json.html"
                },{
                    "id": "/mq/2019/10/02/rabbitmq.html",
                    "name": "RabbitMQ",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/mq/2019/10/02/rabbitmq.html"
                },{
                    "id": "/mq/2019/10/02/activemq.html",
                    "name": "ActiveMQ",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/mq/2019/10/02/activemq.html"
                },{
                    "id": "/java/2019/08/09/javase.html",
                    "name": "JavaSE",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/java/2019/08/09/javase.html"
                },{
                    "id": "/%E7%BD%91%E7%BB%9C/2019/07/10/frp.html",
                    "name": "frp All in One",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E7%BD%91%E7%BB%9C/2019/07/10/frp.html"
                },{
                    "id": "/db/2019/07/08/jpa.html",
                    "name": "JPA All in One",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/db/2019/07/08/jpa.html"
                },{
                    "id": "/%E5%AE%B9%E5%99%A8%E4%BA%91/2019/06/10/docker.html",
                    "name": "Docker All in One",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%AE%B9%E5%99%A8%E4%BA%91/2019/06/10/docker.html"
                },{
                    "id": "/%E7%BD%91%E7%BB%9C/2019/05/06/nginx.html",
                    "name": "NginX All in One",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E7%BD%91%E7%BB%9C/2019/05/06/nginx.html"
                },{
                    "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2019/05/04/idea.html",
                    "name": "IntelliJ IDEA常用快捷键",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2019/05/04/idea.html"
                },{
                    "id": "/mq/2019/03/04/zookeeper.html",
                    "name": "zookeeper集群",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/mq/2019/03/04/zookeeper.html"
                },{
                    "id": "/mq/2019/03/04/kafka.html",
                    "name": "Kafka集群",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/mq/2019/03/04/kafka.html"
                },{
                    "id": "/db/2019/01/01/dbms-design.html",
                    "name": "数据库设计方案",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/db/2019/01/01/dbms-design.html"
                },{
                    "id": "/db/2018/10/06/oracle.html",
                    "name": "Oracle All in One",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/db/2018/10/06/oracle.html"
                },{
                    "id": "/db/2018/10/05/mysql.html",
                    "name": "MySQL All in One",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/db/2018/10/05/mysql.html"
                },{
                    "id": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2018/08/12/design-patterns.html",
                    "name": "设计模式新解读",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2018/08/12/design-patterns.html"
                },{
                    "id": "/db/2018/06/18/powerdesigner.html",
                    "name": "PowerDesigner",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/db/2018/06/18/powerdesigner.html"
                },{
                    "id": "/tools/2018/06/07/shadowsocks.html",
                    "name": "科学上网",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/tools/2018/06/07/shadowsocks.html"
                },{
                    "id": "/javascript/2018/04/23/javascript.html",
                    "name": "javascript",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/javascript/2018/04/23/javascript.html"
                },{
                    "id": "/spring-cloud/2018/04/05/spring.html",
                    "name": "Spring All in One",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/spring-cloud/2018/04/05/spring.html"
                },{
                    "id": "/db/2018/03/19/memcached.html",
                    "name": "memcached",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/db/2018/03/19/memcached.html"
                },{
                    "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2018/03/15/log.html",
                    "name": "Log All in One",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2018/03/15/log.html"
                },{
                    "id": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2018/02/03/java-blog.html",
                    "name": "基于Java的个人博客系统探索",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2018/02/03/java-blog.html"
                },{
                    "id": "/tools/2018/01/12/markdown.html",
                    "name": "markdown all in one",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/tools/2018/01/12/markdown.html"
                },{
                    "id": "/%E7%B3%BB%E7%BB%9F/2017/10/27/osx.html",
                    "name": "MacOS 使用记录",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E7%B3%BB%E7%BB%9F/2017/10/27/osx.html"
                },{
                    "id": "/linux/2017/10/03/linux-shell.html",
                    "name": "shell 脚本使用",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/linux/2017/10/03/linux-shell.html"
                },{
                    "id": "/linux/2017/10/02/linux-vi.html",
                    "name": "Linux VI 大全",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/linux/2017/10/02/linux-vi.html"
                },{
                    "id": "/linux/2017/10/01/linux.html",
                    "name": "Linux 常用命令",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/linux/2017/10/01/linux.html"
                },{
                    "id": "/%E7%B3%BB%E7%BB%9F/2017/01/01/windows.html",
                    "name": "Windows All in One",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E7%B3%BB%E7%BB%9F/2017/01/01/windows.html"
                },{
                    "id": "/tools/2016/07/01/onenote.html",
                    "name": "Onenote",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/tools/2016/07/01/onenote.html"
                },{
                    "id": "/spring-cloud/2016/06/02/sys-spring-boot-starter.html",
                    "name": "sys spring boot starter",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/spring-cloud/2016/06/02/sys-spring-boot-starter.html"
                },{
                    "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2012/12/07/jar-starter.html",
                    "name": "jar包启动工具脚本",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2012/12/07/jar-starter.html"
                },{
                    "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2001/01/01/virtualbox.html",
                    "name": "VirtualBox",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2001/01/01/virtualbox.html"
                },{
                    "id": "/personal/1991/07/10/resume.html",
                    "name": "简历",
                    "value": "文章",
                    "category": "文章",
                    "label": {"show": true},
                    "symbolSize": 10,
                    "symbol": 'circle',
                    "x": randomX(),
                    "y": randomY(),
                    "url": "/personal/1991/07/10/resume.html"
                },]

        let nodes_tag = [{
                        "id": "info",
                        "name": "info",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/info.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "resume",
                        "name": "resume",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/resume.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "vm",
                        "name": "vm",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/vm.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "tools",
                        "name": "tools",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/tools.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "spring",
                        "name": "spring",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/spring.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "onenote",
                        "name": "onenote",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/onenote.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "windows",
                        "name": "windows",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/windows.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "linux",
                        "name": "linux",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/linux.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "vi",
                        "name": "vi",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/vi.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "shell",
                        "name": "shell",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/shell.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "MacOS",
                        "name": "MacOS",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/macos.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "OSX",
                        "name": "OSX",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/osx.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "markdown",
                        "name": "markdown",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/markdown.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "博客",
                        "name": "博客",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/博客.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "log",
                        "name": "log",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/log.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "日志",
                        "name": "日志",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/日志.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "memcached",
                        "name": "memcached",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/memcached.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "nodejs",
                        "name": "nodejs",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/nodejs.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "vue",
                        "name": "vue",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/vue.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "node.js",
                        "name": "node.js",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/node.js.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "ss",
                        "name": "ss",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/ss.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "shadowsocks",
                        "name": "shadowsocks",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/shadowsocks.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "PowerDesigner",
                        "name": "PowerDesigner",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/powerdesigner.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "设计模式",
                        "name": "设计模式",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/设计模式.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "mysql",
                        "name": "mysql",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/mysql.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "oracle",
                        "name": "oracle",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/oracle.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "kafka",
                        "name": "kafka",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/kafka.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "zookeeper",
                        "name": "zookeeper",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/zookeeper.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "idea",
                        "name": "idea",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/idea.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "nginx",
                        "name": "nginx",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/nginx.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "docker",
                        "name": "docker",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/docker.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "jpa",
                        "name": "jpa",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/jpa.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "frp",
                        "name": "frp",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/frp.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "java",
                        "name": "java",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/java.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "ActiveMQ",
                        "name": "ActiveMQ",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/activemq.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "RabbitMQ",
                        "name": "RabbitMQ",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/rabbitmq.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "json",
                        "name": "json",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/json.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "jrebel",
                        "name": "jrebel",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/jrebel.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "mongoDB",
                        "name": "mongoDB",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/mongodb.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "redis",
                        "name": "redis",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/redis.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "maven",
                        "name": "maven",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/maven.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "jvm",
                        "name": "jvm",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/jvm.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "jekyll",
                        "name": "jekyll",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/jekyll.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "GitHub-Pages",
                        "name": "GitHub-Pages",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/github-pages.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "efk",
                        "name": "efk",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/efk.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "elk",
                        "name": "elk",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/elk.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "git",
                        "name": "git",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/git.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "github",
                        "name": "github",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/github.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "gitlab",
                        "name": "gitlab",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/gitlab.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "vcs",
                        "name": "vcs",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/vcs.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "OCR",
                        "name": "OCR",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/ocr.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "tesseract",
                        "name": "tesseract",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/tesseract.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "flink",
                        "name": "flink",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/flink.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "inmgr",
                        "name": "inmgr",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/inmgr.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "api",
                        "name": "api",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/api.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "个人理财",
                        "name": "个人理财",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/个人理财.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "电影",
                        "name": "电影",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/电影.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "为人处事",
                        "name": "为人处事",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/为人处事.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "pinpoint",
                        "name": "pinpoint",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/pinpoint.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "APM",
                        "name": "APM",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/apm.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "skywalking",
                        "name": "skywalking",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/skywalking.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "Jenkins",
                        "name": "Jenkins",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/jenkins.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "bigdata",
                        "name": "bigdata",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/bigdata.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "hadoop",
                        "name": "hadoop",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/hadoop.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "茄子",
                        "name": "茄子",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/茄子.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "eggplant",
                        "name": "eggplant",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/eggplant.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "ssh",
                        "name": "ssh",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/ssh.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "test",
                        "name": "test",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/test.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "测试",
                        "name": "测试",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/测试.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "ddp",
                        "name": "ddp",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/ddp.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "访问者模式",
                        "name": "访问者模式",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/访问者模式.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "sublime",
                        "name": "sublime",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/sublime.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "es",
                        "name": "es",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/es.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "elasticsearch",
                        "name": "elasticsearch",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/elasticsearch.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "工具",
                        "name": "工具",
                        "value": "标签",
                        "category": "标签",
                        "label": {"show": false},
                        "symbolSize": 20,
                        "symbol": 'image://assets/icon/工具.png',
                        "x": randomX(),
                        "y": randomY()
                    },]

        let nodes_cat = [{
                        "id": "personal",
                        "name": "personal",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/personal.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "开发运维",
                        "name": "开发运维",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/开发运维.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "spring-cloud",
                        "name": "spring-cloud",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/spring-cloud.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "tools",
                        "name": "tools",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/tools.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "系统",
                        "name": "系统",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/系统.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "Linux",
                        "name": "Linux",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/linux.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "博客建设",
                        "name": "博客建设",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/博客建设.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "大数据",
                        "name": "大数据",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/大数据.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "DB",
                        "name": "DB",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/db.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "javascript",
                        "name": "javascript",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/javascript.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "设计模式",
                        "name": "设计模式",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/设计模式.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "MQ",
                        "name": "MQ",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/mq.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "网络",
                        "name": "网络",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/网络.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "容器云",
                        "name": "容器云",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/容器云.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "Java",
                        "name": "Java",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/java.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "代码",
                        "name": "代码",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/代码.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "inmgr",
                        "name": "inmgr",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/inmgr.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "吃喝玩乐",
                        "name": "吃喝玩乐",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/吃喝玩乐.png',
                        "x": randomX(),
                        "y": randomY()
                    },{
                        "id": "工具",
                        "name": "工具",
                        "value": "分类",
                        "category": "分类",
                        "label": {"show": false},
                        "symbolSize": 35,
                        "symbol": 'image://assets/icon/工具.png',
                        "x": randomX(),
                        "y": randomY()
                    },]

        // imjcker 跟节点
        let root_node = [
            {
                "id": "imjcker",
                "name": "百年孤独",
                "value": "category",
                "category": "分类",
                "label": {"show": false},
                "symbolSize": 50,
                "symbol": 'image://assets/favicon.ico',
                "x": randomX(),
                "y": randomY()
            }
        ]
        let nodes = uniqueBy(Array.from(new Set(root_node.concat(nodes_cat).concat(nodes_tag).concat(nodes_post))), 'id');



        let links_c_root = [{
            "source": "personal",
            "target": "imjcker"
        },{
            "source": "开发运维",
            "target": "imjcker"
        },{
            "source": "spring-cloud",
            "target": "imjcker"
        },{
            "source": "tools",
            "target": "imjcker"
        },{
            "source": "系统",
            "target": "imjcker"
        },{
            "source": "Linux",
            "target": "imjcker"
        },{
            "source": "博客建设",
            "target": "imjcker"
        },{
            "source": "大数据",
            "target": "imjcker"
        },{
            "source": "DB",
            "target": "imjcker"
        },{
            "source": "javascript",
            "target": "imjcker"
        },{
            "source": "设计模式",
            "target": "imjcker"
        },{
            "source": "MQ",
            "target": "imjcker"
        },{
            "source": "网络",
            "target": "imjcker"
        },{
            "source": "容器云",
            "target": "imjcker"
        },{
            "source": "Java",
            "target": "imjcker"
        },{
            "source": "代码",
            "target": "imjcker"
        },{
            "source": "inmgr",
            "target": "imjcker"
        },{
            "source": "吃喝玩乐",
            "target": "imjcker"
        },{
            "source": "工具",
            "target": "imjcker"
        },]
        let links_t_p = [{
                "source": "/personal/1991/07/10/resume.html",
                "target": "info"
            },{
                "source": "/personal/1991/07/10/resume.html",
                "target": "resume"
            },{
                "source": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2001/01/01/virtualbox.html",
                "target": "vm"
            },{
                "source": "/tools/2021/12/05/ddns.html",
                "target": "tools"
            },{
                "source": "/tools/2021/12/03/nacos.html",
                "target": "tools"
            },{
                "source": "/tools/2021/12/01/docsify.html",
                "target": "tools"
            },{
                "source": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2012/12/07/jar-starter.html",
                "target": "tools"
            },{
                "source": "/spring-cloud/2018/04/05/spring.html",
                "target": "spring"
            },{
                "source": "/spring-cloud/2016/06/02/sys-spring-boot-starter.html",
                "target": "spring"
            },{
                "source": "/tools/2016/07/01/onenote.html",
                "target": "onenote"
            },{
                "source": "/%E7%B3%BB%E7%BB%9F/2017/01/01/windows.html",
                "target": "windows"
            },{
                "source": "/linux/2017/10/02/linux-vi.html",
                "target": "linux"
            },{
                "source": "/linux/2017/10/01/linux.html",
                "target": "linux"
            },{
                "source": "/linux/2017/10/02/linux-vi.html",
                "target": "vi"
            },{
                "source": "/linux/2017/10/03/linux-shell.html",
                "target": "shell"
            },{
                "source": "/%E7%B3%BB%E7%BB%9F/2017/10/27/osx.html",
                "target": "MacOS"
            },{
                "source": "/%E7%B3%BB%E7%BB%9F/2017/10/27/osx.html",
                "target": "OSX"
            },{
                "source": "/tools/2018/01/12/markdown.html",
                "target": "markdown"
            },{
                "source": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2020/01/17/static-pages-based-on-jekyll.html",
                "target": "博客"
            },{
                "source": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2018/02/03/java-blog.html",
                "target": "博客"
            },{
                "source": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2018/03/15/log.html",
                "target": "log"
            },{
                "source": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2018/03/15/log.html",
                "target": "日志"
            },{
                "source": "/db/2018/03/19/memcached.html",
                "target": "memcached"
            },{
                "source": "/javascript/2018/04/23/javascript.html",
                "target": "nodejs"
            },{
                "source": "/javascript/2018/04/23/javascript.html",
                "target": "vue"
            },{
                "source": "/javascript/2018/04/23/javascript.html",
                "target": "node.js"
            },{
                "source": "/tools/2018/06/07/shadowsocks.html",
                "target": "ss"
            },{
                "source": "/tools/2018/06/07/shadowsocks.html",
                "target": "shadowsocks"
            },{
                "source": "/db/2018/06/18/powerdesigner.html",
                "target": "PowerDesigner"
            },{
                "source": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2020/06/01/ddp.html",
                "target": "设计模式"
            },{
                "source": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2018/08/12/design-patterns.html",
                "target": "设计模式"
            },{
                "source": "/db/2019/01/01/dbms-design.html",
                "target": "mysql"
            },{
                "source": "/db/2018/10/05/mysql.html",
                "target": "mysql"
            },{
                "source": "/db/2019/01/01/dbms-design.html",
                "target": "oracle"
            },{
                "source": "/db/2018/10/06/oracle.html",
                "target": "oracle"
            },{
                "source": "/mq/2019/03/04/kafka.html",
                "target": "kafka"
            },{
                "source": "/mq/2019/03/04/zookeeper.html",
                "target": "zookeeper"
            },{
                "source": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2019/05/04/idea.html",
                "target": "idea"
            },{
                "source": "/%E7%BD%91%E7%BB%9C/2019/05/06/nginx.html",
                "target": "nginx"
            },{
                "source": "/%E5%AE%B9%E5%99%A8%E4%BA%91/2019/06/10/docker.html",
                "target": "docker"
            },{
                "source": "/db/2019/07/08/jpa.html",
                "target": "jpa"
            },{
                "source": "/%E7%BD%91%E7%BB%9C/2019/07/10/frp.html",
                "target": "frp"
            },{
                "source": "/java/2019/08/09/javase.html",
                "target": "java"
            },{
                "source": "/mq/2019/10/02/activemq.html",
                "target": "ActiveMQ"
            },{
                "source": "/mq/2019/10/02/rabbitmq.html",
                "target": "RabbitMQ"
            },{
                "source": "/%E4%BB%A3%E7%A0%81/2019/12/21/json.html",
                "target": "json"
            },{
                "source": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2019/12/31/jrebel-license-server.html",
                "target": "jrebel"
            },{
                "source": "/db/2020/01/01/mongodb.html",
                "target": "mongoDB"
            },{
                "source": "/db/2020/01/01/redis.html",
                "target": "redis"
            },{
                "source": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/01/02/maven.html",
                "target": "maven"
            },{
                "source": "/java/2020/01/12/jvm.html",
                "target": "jvm"
            },{
                "source": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2020/01/17/static-pages-based-on-jekyll.html",
                "target": "jekyll"
            },{
                "source": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2020/01/17/static-pages-based-on-jekyll.html",
                "target": "GitHub-Pages"
            },{
                "source": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/19/efk.html",
                "target": "efk"
            },{
                "source": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/19/efk.html",
                "target": "elk"
            },{
                "source": "/%E4%BB%A3%E7%A0%81/2020/01/19/git.html",
                "target": "git"
            },{
                "source": "/%E4%BB%A3%E7%A0%81/2020/01/19/git.html",
                "target": "github"
            },{
                "source": "/%E4%BB%A3%E7%A0%81/2020/01/19/git.html",
                "target": "gitlab"
            },{
                "source": "/%E4%BB%A3%E7%A0%81/2020/01/19/git.html",
                "target": "vcs"
            },{
                "source": "/tools/2020/01/20/tesseract.html",
                "target": "OCR"
            },{
                "source": "/tools/2020/01/20/tesseract.html",
                "target": "tesseract"
            },{
                "source": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/21/Flink-All-in-one.html",
                "target": "flink"
            },{
                "source": "/inmgr/2020/02/14/the-future-of-inmgr.html",
                "target": "inmgr"
            },{
                "source": "/inmgr/2020/02/14/the-future-of-inmgr.html",
                "target": "api"
            },{
                "source": "/personal/2020/02/16/fire.html",
                "target": "个人理财"
            },{
                "source": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/02/17/Once-Upon-a-Time-in-Hollywood.html",
                "target": "电影"
            },{
                "source": "/personal/2020/03/07/the-art-of-talk.html",
                "target": "为人处事"
            },{
                "source": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/03/apm.html",
                "target": "pinpoint"
            },{
                "source": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/03/apm.html",
                "target": "APM"
            },{
                "source": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/03/apm.html",
                "target": "skywalking"
            },{
                "source": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/11/ci.html",
                "target": "Jenkins"
            },{
                "source": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/04/12/hadoop.html",
                "target": "bigdata"
            },{
                "source": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/04/12/hadoop.html",
                "target": "hadoop"
            },{
                "source": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/04/19/eggplant.html",
                "target": "茄子"
            },{
                "source": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/04/19/eggplant.html",
                "target": "eggplant"
            },{
                "source": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/19/ssh.html",
                "target": "ssh"
            },{
                "source": "/linux/2020/05/06/test-all-in-one.html",
                "target": "test"
            },{
                "source": "/linux/2020/05/06/arthas.html",
                "target": "test"
            },{
                "source": "/linux/2020/05/06/test-all-in-one.html",
                "target": "测试"
            },{
                "source": "/linux/2020/05/06/arthas.html",
                "target": "测试"
            },{
                "source": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2020/06/01/ddp.html",
                "target": "ddp"
            },{
                "source": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2020/06/01/ddp.html",
                "target": "访问者模式"
            },{
                "source": "/%E5%B7%A5%E5%85%B7/2020/06/17/sublime.html",
                "target": "sublime"
            },{
                "source": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/11/17/es.html",
                "target": "es"
            },{
                "source": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/11/17/es.html",
                "target": "elasticsearch"
            },{
                "source": "/tools/2021/12/05/ddns.html",
                "target": "工具"
            },{
                "source": "/tools/2021/12/03/nacos.html",
                "target": "工具"
            },{
                "source": "/tools/2021/12/01/docsify.html",
                "target": "工具"
            },]
        let links_c_t = [{
                "source": "tools",
                "target": "tools"
            },{
                "source": "工具",
                "target": "tools"
            },{
                "source": "tools",
                "target": "tools"
            },{
                "source": "工具",
                "target": "tools"
            },{
                "source": "tools",
                "target": "tools"
            },{
                "source": "工具",
                "target": "tools"
            },{
                "source": "es",
                "target": "大数据"
            },{
                "source": "elasticsearch",
                "target": "大数据"
            },{
                "source": "sublime",
                "target": "工具"
            },{
                "source": "ddp",
                "target": "设计模式"
            },{
                "source": "设计模式",
                "target": "设计模式"
            },{
                "source": "访问者模式",
                "target": "设计模式"
            },{
                "source": "test",
                "target": "Linux"
            },{
                "source": "测试",
                "target": "Linux"
            },{
                "source": "test",
                "target": "Linux"
            },{
                "source": "测试",
                "target": "Linux"
            },{
                "source": "ssh",
                "target": "开发运维"
            },{
                "source": "茄子",
                "target": "吃喝玩乐"
            },{
                "source": "eggplant",
                "target": "吃喝玩乐"
            },{
                "source": "bigdata",
                "target": "大数据"
            },{
                "source": "hadoop",
                "target": "大数据"
            },{
                "source": "Jenkins",
                "target": "开发运维"
            },{
                "source": "pinpoint",
                "target": "开发运维"
            },{
                "source": "APM",
                "target": "开发运维"
            },{
                "source": "skywalking",
                "target": "开发运维"
            },{
                "source": "为人处事",
                "target": "personal"
            },{
                "source": "电影",
                "target": "吃喝玩乐"
            },{
                "source": "个人理财",
                "target": "personal"
            },{
                "source": "inmgr",
                "target": "inmgr"
            },{
                "source": "api",
                "target": "inmgr"
            },{
                "source": "flink",
                "target": "大数据"
            },{
                "source": "OCR",
                "target": "tools"
            },{
                "source": "tesseract",
                "target": "tools"
            },{
                "source": "git",
                "target": "代码"
            },{
                "source": "github",
                "target": "代码"
            },{
                "source": "gitlab",
                "target": "代码"
            },{
                "source": "vcs",
                "target": "代码"
            },{
                "source": "efk",
                "target": "大数据"
            },{
                "source": "elk",
                "target": "大数据"
            },{
                "source": "博客",
                "target": "博客建设"
            },{
                "source": "jekyll",
                "target": "博客建设"
            },{
                "source": "GitHub-Pages",
                "target": "博客建设"
            },{
                "source": "jvm",
                "target": "Java"
            },{
                "source": "maven",
                "target": "开发运维"
            },{
                "source": "redis",
                "target": "DB"
            },{
                "source": "mongoDB",
                "target": "DB"
            },{
                "source": "jrebel",
                "target": "开发运维"
            },{
                "source": "json",
                "target": "代码"
            },{
                "source": "RabbitMQ",
                "target": "MQ"
            },{
                "source": "ActiveMQ",
                "target": "MQ"
            },{
                "source": "java",
                "target": "Java"
            },{
                "source": "frp",
                "target": "网络"
            },{
                "source": "jpa",
                "target": "DB"
            },{
                "source": "docker",
                "target": "容器云"
            },{
                "source": "nginx",
                "target": "网络"
            },{
                "source": "idea",
                "target": "开发运维"
            },{
                "source": "zookeeper",
                "target": "MQ"
            },{
                "source": "kafka",
                "target": "MQ"
            },{
                "source": "oracle",
                "target": "DB"
            },{
                "source": "mysql",
                "target": "DB"
            },{
                "source": "oracle",
                "target": "DB"
            },{
                "source": "mysql",
                "target": "DB"
            },{
                "source": "设计模式",
                "target": "设计模式"
            },{
                "source": "PowerDesigner",
                "target": "DB"
            },{
                "source": "ss",
                "target": "tools"
            },{
                "source": "shadowsocks",
                "target": "tools"
            },{
                "source": "nodejs",
                "target": "javascript"
            },{
                "source": "vue",
                "target": "javascript"
            },{
                "source": "node.js",
                "target": "javascript"
            },{
                "source": "spring",
                "target": "spring-cloud"
            },{
                "source": "memcached",
                "target": "DB"
            },{
                "source": "log",
                "target": "大数据"
            },{
                "source": "日志",
                "target": "大数据"
            },{
                "source": "博客",
                "target": "博客建设"
            },{
                "source": "markdown",
                "target": "tools"
            },{
                "source": "MacOS",
                "target": "系统"
            },{
                "source": "OSX",
                "target": "系统"
            },{
                "source": "shell",
                "target": "Linux"
            },{
                "source": "linux",
                "target": "Linux"
            },{
                "source": "vi",
                "target": "Linux"
            },{
                "source": "linux",
                "target": "Linux"
            },{
                "source": "windows",
                "target": "系统"
            },{
                "source": "onenote",
                "target": "tools"
            },{
                "source": "spring",
                "target": "spring-cloud"
            },{
                "source": "tools",
                "target": "开发运维"
            },{
                "source": "vm",
                "target": "开发运维"
            },{
                "source": "info",
                "target": "personal"
            },{
                "source": "resume",
                "target": "personal"
            },]
        let links = links_t_p.concat(links_c_t).concat(links_c_root);

        // show clicked category
        let hash = decodeURI(document.location.hash.toString().substr(1));
        if (hash === ''){
            return {
                "categories": categories,
                "links": links,
                "nodes": nodes
            }
        }

        if (hash.startsWith('c-')){
            let cat = hash.substr(2)
            // 过滤分类节点
            nodes_cat = nodes_cat.filter(function(item){
                return item.name === cat;
            });
            // 过滤文章节点
            nodes_post = [{
                        "id": "/personal/2020/03/07/the-art-of-talk.html",
                        "name": "说话的艺术",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/personal/2020/03/07/the-art-of-talk.html",
                        "ccc": "personal"
                    },{
                        "id": "/personal/2020/02/16/fire.html",
                        "name": "FIRE",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/personal/2020/02/16/fire.html",
                        "ccc": "personal"
                    },{
                        "id": "/personal/1991/07/10/resume.html",
                        "name": "简历",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/personal/1991/07/10/resume.html",
                        "ccc": "personal"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/19/ssh.html",
                        "name": "SSH免密登录",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/19/ssh.html",
                        "ccc": "开发运维"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/11/ci.html",
                        "name": "Jenkins 环境搭建",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/11/ci.html",
                        "ccc": "开发运维"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/03/apm.html",
                        "name": "APM搭建使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/03/apm.html",
                        "ccc": "开发运维"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/01/02/maven.html",
                        "name": "Maven All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/01/02/maven.html",
                        "ccc": "开发运维"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2019/12/31/jrebel-license-server.html",
                        "name": "Jrebel激活服务",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2019/12/31/jrebel-license-server.html",
                        "ccc": "开发运维"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2019/05/04/idea.html",
                        "name": "IntelliJ IDEA常用快捷键",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2019/05/04/idea.html",
                        "ccc": "开发运维"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2012/12/07/jar-starter.html",
                        "name": "jar包启动工具脚本",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2012/12/07/jar-starter.html",
                        "ccc": "开发运维"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2001/01/01/virtualbox.html",
                        "name": "VirtualBox",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2001/01/01/virtualbox.html",
                        "ccc": "开发运维"
                    },{
                        "id": "/spring-cloud/2018/04/05/spring.html",
                        "name": "Spring All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/spring-cloud/2018/04/05/spring.html",
                        "ccc": "spring-cloud"
                    },{
                        "id": "/spring-cloud/2016/06/02/sys-spring-boot-starter.html",
                        "name": "sys spring boot starter",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/spring-cloud/2016/06/02/sys-spring-boot-starter.html",
                        "ccc": "spring-cloud"
                    },{
                        "id": "/tools/2021/12/05/ddns.html",
                        "name": "ddns",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2021/12/05/ddns.html",
                        "ccc": "tools"
                    },{
                        "id": "/tools/2021/12/03/nacos.html",
                        "name": "nacos",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2021/12/03/nacos.html",
                        "ccc": "tools"
                    },{
                        "id": "/tools/2021/12/01/docsify.html",
                        "name": "docsify打包docker镜像",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2021/12/01/docsify.html",
                        "ccc": "tools"
                    },{
                        "id": "/tools/2020/01/20/tesseract.html",
                        "name": "Tesseract 使用记录",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2020/01/20/tesseract.html",
                        "ccc": "tools"
                    },{
                        "id": "/tools/2018/06/07/shadowsocks.html",
                        "name": "科学上网",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2018/06/07/shadowsocks.html",
                        "ccc": "tools"
                    },{
                        "id": "/tools/2018/01/12/markdown.html",
                        "name": "markdown all in one",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2018/01/12/markdown.html",
                        "ccc": "tools"
                    },{
                        "id": "/tools/2016/07/01/onenote.html",
                        "name": "Onenote",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2016/07/01/onenote.html",
                        "ccc": "tools"
                    },{
                        "id": "/%E7%B3%BB%E7%BB%9F/2017/10/27/osx.html",
                        "name": "MacOS 使用记录",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E7%B3%BB%E7%BB%9F/2017/10/27/osx.html",
                        "ccc": "系统"
                    },{
                        "id": "/%E7%B3%BB%E7%BB%9F/2017/01/01/windows.html",
                        "name": "Windows All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E7%B3%BB%E7%BB%9F/2017/01/01/windows.html",
                        "ccc": "系统"
                    },{
                        "id": "/linux/2020/05/06/test-all-in-one.html",
                        "name": "测试工具使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/linux/2020/05/06/test-all-in-one.html",
                        "ccc": "Linux"
                    },{
                        "id": "/linux/2020/05/06/arthas.html",
                        "name": "Arthas使用教程",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/linux/2020/05/06/arthas.html",
                        "ccc": "Linux"
                    },{
                        "id": "/linux/2017/10/03/linux-shell.html",
                        "name": "shell 脚本使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/linux/2017/10/03/linux-shell.html",
                        "ccc": "Linux"
                    },{
                        "id": "/linux/2017/10/02/linux-vi.html",
                        "name": "Linux VI 大全",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/linux/2017/10/02/linux-vi.html",
                        "ccc": "Linux"
                    },{
                        "id": "/linux/2017/10/01/linux.html",
                        "name": "Linux 常用命令",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/linux/2017/10/01/linux.html",
                        "ccc": "Linux"
                    },{
                        "id": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2020/01/17/static-pages-based-on-jekyll.html",
                        "name": "Jekyll静态博客",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2020/01/17/static-pages-based-on-jekyll.html",
                        "ccc": "博客建设"
                    },{
                        "id": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2018/02/03/java-blog.html",
                        "name": "基于Java的个人博客系统探索",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2018/02/03/java-blog.html",
                        "ccc": "博客建设"
                    },{
                        "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/11/17/es.html",
                        "name": "ES数据操作",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/11/17/es.html",
                        "ccc": "大数据"
                    },{
                        "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/04/12/hadoop.html",
                        "name": "Hadoop 搭建",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/04/12/hadoop.html",
                        "ccc": "大数据"
                    },{
                        "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/21/Flink-All-in-one.html",
                        "name": "Flink All in one",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/21/Flink-All-in-one.html",
                        "ccc": "大数据"
                    },{
                        "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/19/efk.html",
                        "name": "EFK 搭建使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/19/efk.html",
                        "ccc": "大数据"
                    },{
                        "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2018/03/15/log.html",
                        "name": "Log All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2018/03/15/log.html",
                        "ccc": "大数据"
                    },{
                        "id": "/db/2020/01/01/redis.html",
                        "name": "redis",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2020/01/01/redis.html",
                        "ccc": "DB"
                    },{
                        "id": "/db/2020/01/01/mongodb.html",
                        "name": "MongoDB",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2020/01/01/mongodb.html",
                        "ccc": "DB"
                    },{
                        "id": "/db/2019/07/08/jpa.html",
                        "name": "JPA All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2019/07/08/jpa.html",
                        "ccc": "DB"
                    },{
                        "id": "/db/2019/01/01/dbms-design.html",
                        "name": "数据库设计方案",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2019/01/01/dbms-design.html",
                        "ccc": "DB"
                    },{
                        "id": "/db/2018/10/06/oracle.html",
                        "name": "Oracle All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2018/10/06/oracle.html",
                        "ccc": "DB"
                    },{
                        "id": "/db/2018/10/05/mysql.html",
                        "name": "MySQL All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2018/10/05/mysql.html",
                        "ccc": "DB"
                    },{
                        "id": "/db/2018/06/18/powerdesigner.html",
                        "name": "PowerDesigner",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2018/06/18/powerdesigner.html",
                        "ccc": "DB"
                    },{
                        "id": "/db/2018/03/19/memcached.html",
                        "name": "memcached",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2018/03/19/memcached.html",
                        "ccc": "DB"
                    },{
                        "id": "/javascript/2018/04/23/javascript.html",
                        "name": "javascript",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/javascript/2018/04/23/javascript.html",
                        "ccc": "javascript"
                    },{
                        "id": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2020/06/01/ddp.html",
                        "name": "设计模式-访问者模式",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2020/06/01/ddp.html",
                        "ccc": "设计模式"
                    },{
                        "id": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2018/08/12/design-patterns.html",
                        "name": "设计模式新解读",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2018/08/12/design-patterns.html",
                        "ccc": "设计模式"
                    },{
                        "id": "/mq/2019/10/02/rabbitmq.html",
                        "name": "RabbitMQ",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/mq/2019/10/02/rabbitmq.html",
                        "ccc": "MQ"
                    },{
                        "id": "/mq/2019/10/02/activemq.html",
                        "name": "ActiveMQ",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/mq/2019/10/02/activemq.html",
                        "ccc": "MQ"
                    },{
                        "id": "/mq/2019/03/04/zookeeper.html",
                        "name": "zookeeper集群",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/mq/2019/03/04/zookeeper.html",
                        "ccc": "MQ"
                    },{
                        "id": "/mq/2019/03/04/kafka.html",
                        "name": "Kafka集群",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/mq/2019/03/04/kafka.html",
                        "ccc": "MQ"
                    },{
                        "id": "/%E7%BD%91%E7%BB%9C/2019/07/10/frp.html",
                        "name": "frp All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E7%BD%91%E7%BB%9C/2019/07/10/frp.html",
                        "ccc": "网络"
                    },{
                        "id": "/%E7%BD%91%E7%BB%9C/2019/05/06/nginx.html",
                        "name": "NginX All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E7%BD%91%E7%BB%9C/2019/05/06/nginx.html",
                        "ccc": "网络"
                    },{
                        "id": "/%E5%AE%B9%E5%99%A8%E4%BA%91/2019/06/10/docker.html",
                        "name": "Docker All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%AE%B9%E5%99%A8%E4%BA%91/2019/06/10/docker.html",
                        "ccc": "容器云"
                    },{
                        "id": "/java/2020/01/12/jvm.html",
                        "name": "Java All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/java/2020/01/12/jvm.html",
                        "ccc": "Java"
                    },{
                        "id": "/java/2019/08/09/javase.html",
                        "name": "JavaSE",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/java/2019/08/09/javase.html",
                        "ccc": "Java"
                    },{
                        "id": "/%E4%BB%A3%E7%A0%81/2020/01/19/git.html",
                        "name": "Git 操作使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E4%BB%A3%E7%A0%81/2020/01/19/git.html",
                        "ccc": "代码"
                    },{
                        "id": "/%E4%BB%A3%E7%A0%81/2019/12/21/json.html",
                        "name": "Json All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E4%BB%A3%E7%A0%81/2019/12/21/json.html",
                        "ccc": "代码"
                    },{
                        "id": "/inmgr/2020/02/14/the-future-of-inmgr.html",
                        "name": "接口平台的反思与发展",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/inmgr/2020/02/14/the-future-of-inmgr.html",
                        "ccc": "inmgr"
                    },{
                        "id": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/04/19/eggplant.html",
                        "name": "风味茄子",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/04/19/eggplant.html",
                        "ccc": "吃喝玩乐"
                    },{
                        "id": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/02/17/Once-Upon-a-Time-in-Hollywood.html",
                        "name": "好莱坞往事",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/02/17/Once-Upon-a-Time-in-Hollywood.html",
                        "ccc": "吃喝玩乐"
                    },{
                        "id": "/%E5%B7%A5%E5%85%B7/2020/06/17/sublime.html",
                        "name": "Sublime 快捷键",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%B7%A5%E5%85%B7/2020/06/17/sublime.html",
                        "ccc": "工具"
                    },].filter(function (item) {
                    return item.ccc === cat
                });

            // 寻找target为hash的link，然后通过这批link的source过滤tags节点
            let links_t_c = links.filter(function (link) {
                return link.target === cat;// || link.source === cat;
            })
            // 过滤标签节点
            nodes_tag = nodes_tag.filter(function (node) {
                return  links_t_c.find((value) => value.source === node.name)
            })
            //合并节点
            nodes = nodes_cat.concat(nodes_tag).concat(nodes_post);
        } else if (hash.startsWith('t-')){
            let tag = hash.substr(2)
            nodes_tag = nodes_tag.filter(function (node){
                return node.name === tag;
            });

            nodes_post = [{
                        "id": "/personal/1991/07/10/resume.html",
                        "name": "简历",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/personal/1991/07/10/resume.html",
                        "ttt": "info"
                    },{
                        "id": "/personal/1991/07/10/resume.html",
                        "name": "简历",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/personal/1991/07/10/resume.html",
                        "ttt": "resume"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2001/01/01/virtualbox.html",
                        "name": "VirtualBox",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2001/01/01/virtualbox.html",
                        "ttt": "vm"
                    },{
                        "id": "/tools/2021/12/05/ddns.html",
                        "name": "ddns",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2021/12/05/ddns.html",
                        "ttt": "tools"
                    },{
                        "id": "/tools/2021/12/03/nacos.html",
                        "name": "nacos",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2021/12/03/nacos.html",
                        "ttt": "tools"
                    },{
                        "id": "/tools/2021/12/01/docsify.html",
                        "name": "docsify打包docker镜像",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2021/12/01/docsify.html",
                        "ttt": "tools"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2012/12/07/jar-starter.html",
                        "name": "jar包启动工具脚本",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2012/12/07/jar-starter.html",
                        "ttt": "tools"
                    },{
                        "id": "/spring-cloud/2018/04/05/spring.html",
                        "name": "Spring All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/spring-cloud/2018/04/05/spring.html",
                        "ttt": "spring"
                    },{
                        "id": "/spring-cloud/2016/06/02/sys-spring-boot-starter.html",
                        "name": "sys spring boot starter",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/spring-cloud/2016/06/02/sys-spring-boot-starter.html",
                        "ttt": "spring"
                    },{
                        "id": "/tools/2016/07/01/onenote.html",
                        "name": "Onenote",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2016/07/01/onenote.html",
                        "ttt": "onenote"
                    },{
                        "id": "/%E7%B3%BB%E7%BB%9F/2017/01/01/windows.html",
                        "name": "Windows All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E7%B3%BB%E7%BB%9F/2017/01/01/windows.html",
                        "ttt": "windows"
                    },{
                        "id": "/linux/2017/10/02/linux-vi.html",
                        "name": "Linux VI 大全",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/linux/2017/10/02/linux-vi.html",
                        "ttt": "linux"
                    },{
                        "id": "/linux/2017/10/01/linux.html",
                        "name": "Linux 常用命令",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/linux/2017/10/01/linux.html",
                        "ttt": "linux"
                    },{
                        "id": "/linux/2017/10/02/linux-vi.html",
                        "name": "Linux VI 大全",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/linux/2017/10/02/linux-vi.html",
                        "ttt": "vi"
                    },{
                        "id": "/linux/2017/10/03/linux-shell.html",
                        "name": "shell 脚本使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/linux/2017/10/03/linux-shell.html",
                        "ttt": "shell"
                    },{
                        "id": "/%E7%B3%BB%E7%BB%9F/2017/10/27/osx.html",
                        "name": "MacOS 使用记录",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E7%B3%BB%E7%BB%9F/2017/10/27/osx.html",
                        "ttt": "MacOS"
                    },{
                        "id": "/%E7%B3%BB%E7%BB%9F/2017/10/27/osx.html",
                        "name": "MacOS 使用记录",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E7%B3%BB%E7%BB%9F/2017/10/27/osx.html",
                        "ttt": "OSX"
                    },{
                        "id": "/tools/2018/01/12/markdown.html",
                        "name": "markdown all in one",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2018/01/12/markdown.html",
                        "ttt": "markdown"
                    },{
                        "id": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2020/01/17/static-pages-based-on-jekyll.html",
                        "name": "Jekyll静态博客",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2020/01/17/static-pages-based-on-jekyll.html",
                        "ttt": "博客"
                    },{
                        "id": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2018/02/03/java-blog.html",
                        "name": "基于Java的个人博客系统探索",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2018/02/03/java-blog.html",
                        "ttt": "博客"
                    },{
                        "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2018/03/15/log.html",
                        "name": "Log All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2018/03/15/log.html",
                        "ttt": "log"
                    },{
                        "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2018/03/15/log.html",
                        "name": "Log All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2018/03/15/log.html",
                        "ttt": "日志"
                    },{
                        "id": "/db/2018/03/19/memcached.html",
                        "name": "memcached",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2018/03/19/memcached.html",
                        "ttt": "memcached"
                    },{
                        "id": "/javascript/2018/04/23/javascript.html",
                        "name": "javascript",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/javascript/2018/04/23/javascript.html",
                        "ttt": "nodejs"
                    },{
                        "id": "/javascript/2018/04/23/javascript.html",
                        "name": "javascript",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/javascript/2018/04/23/javascript.html",
                        "ttt": "vue"
                    },{
                        "id": "/javascript/2018/04/23/javascript.html",
                        "name": "javascript",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/javascript/2018/04/23/javascript.html",
                        "ttt": "node.js"
                    },{
                        "id": "/tools/2018/06/07/shadowsocks.html",
                        "name": "科学上网",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2018/06/07/shadowsocks.html",
                        "ttt": "ss"
                    },{
                        "id": "/tools/2018/06/07/shadowsocks.html",
                        "name": "科学上网",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2018/06/07/shadowsocks.html",
                        "ttt": "shadowsocks"
                    },{
                        "id": "/db/2018/06/18/powerdesigner.html",
                        "name": "PowerDesigner",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2018/06/18/powerdesigner.html",
                        "ttt": "PowerDesigner"
                    },{
                        "id": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2020/06/01/ddp.html",
                        "name": "设计模式-访问者模式",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2020/06/01/ddp.html",
                        "ttt": "设计模式"
                    },{
                        "id": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2018/08/12/design-patterns.html",
                        "name": "设计模式新解读",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2018/08/12/design-patterns.html",
                        "ttt": "设计模式"
                    },{
                        "id": "/db/2019/01/01/dbms-design.html",
                        "name": "数据库设计方案",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2019/01/01/dbms-design.html",
                        "ttt": "mysql"
                    },{
                        "id": "/db/2018/10/05/mysql.html",
                        "name": "MySQL All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2018/10/05/mysql.html",
                        "ttt": "mysql"
                    },{
                        "id": "/db/2019/01/01/dbms-design.html",
                        "name": "数据库设计方案",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2019/01/01/dbms-design.html",
                        "ttt": "oracle"
                    },{
                        "id": "/db/2018/10/06/oracle.html",
                        "name": "Oracle All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2018/10/06/oracle.html",
                        "ttt": "oracle"
                    },{
                        "id": "/mq/2019/03/04/kafka.html",
                        "name": "Kafka集群",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/mq/2019/03/04/kafka.html",
                        "ttt": "kafka"
                    },{
                        "id": "/mq/2019/03/04/zookeeper.html",
                        "name": "zookeeper集群",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/mq/2019/03/04/zookeeper.html",
                        "ttt": "zookeeper"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2019/05/04/idea.html",
                        "name": "IntelliJ IDEA常用快捷键",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2019/05/04/idea.html",
                        "ttt": "idea"
                    },{
                        "id": "/%E7%BD%91%E7%BB%9C/2019/05/06/nginx.html",
                        "name": "NginX All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E7%BD%91%E7%BB%9C/2019/05/06/nginx.html",
                        "ttt": "nginx"
                    },{
                        "id": "/%E5%AE%B9%E5%99%A8%E4%BA%91/2019/06/10/docker.html",
                        "name": "Docker All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%AE%B9%E5%99%A8%E4%BA%91/2019/06/10/docker.html",
                        "ttt": "docker"
                    },{
                        "id": "/db/2019/07/08/jpa.html",
                        "name": "JPA All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2019/07/08/jpa.html",
                        "ttt": "jpa"
                    },{
                        "id": "/%E7%BD%91%E7%BB%9C/2019/07/10/frp.html",
                        "name": "frp All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E7%BD%91%E7%BB%9C/2019/07/10/frp.html",
                        "ttt": "frp"
                    },{
                        "id": "/java/2019/08/09/javase.html",
                        "name": "JavaSE",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/java/2019/08/09/javase.html",
                        "ttt": "java"
                    },{
                        "id": "/mq/2019/10/02/activemq.html",
                        "name": "ActiveMQ",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/mq/2019/10/02/activemq.html",
                        "ttt": "ActiveMQ"
                    },{
                        "id": "/mq/2019/10/02/rabbitmq.html",
                        "name": "RabbitMQ",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/mq/2019/10/02/rabbitmq.html",
                        "ttt": "RabbitMQ"
                    },{
                        "id": "/%E4%BB%A3%E7%A0%81/2019/12/21/json.html",
                        "name": "Json All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E4%BB%A3%E7%A0%81/2019/12/21/json.html",
                        "ttt": "json"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2019/12/31/jrebel-license-server.html",
                        "name": "Jrebel激活服务",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2019/12/31/jrebel-license-server.html",
                        "ttt": "jrebel"
                    },{
                        "id": "/db/2020/01/01/mongodb.html",
                        "name": "MongoDB",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2020/01/01/mongodb.html",
                        "ttt": "mongoDB"
                    },{
                        "id": "/db/2020/01/01/redis.html",
                        "name": "redis",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/db/2020/01/01/redis.html",
                        "ttt": "redis"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/01/02/maven.html",
                        "name": "Maven All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/01/02/maven.html",
                        "ttt": "maven"
                    },{
                        "id": "/java/2020/01/12/jvm.html",
                        "name": "Java All in One",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/java/2020/01/12/jvm.html",
                        "ttt": "jvm"
                    },{
                        "id": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2020/01/17/static-pages-based-on-jekyll.html",
                        "name": "Jekyll静态博客",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2020/01/17/static-pages-based-on-jekyll.html",
                        "ttt": "jekyll"
                    },{
                        "id": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2020/01/17/static-pages-based-on-jekyll.html",
                        "name": "Jekyll静态博客",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%8D%9A%E5%AE%A2%E5%BB%BA%E8%AE%BE/2020/01/17/static-pages-based-on-jekyll.html",
                        "ttt": "GitHub-Pages"
                    },{
                        "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/19/efk.html",
                        "name": "EFK 搭建使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/19/efk.html",
                        "ttt": "efk"
                    },{
                        "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/19/efk.html",
                        "name": "EFK 搭建使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/19/efk.html",
                        "ttt": "elk"
                    },{
                        "id": "/%E4%BB%A3%E7%A0%81/2020/01/19/git.html",
                        "name": "Git 操作使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E4%BB%A3%E7%A0%81/2020/01/19/git.html",
                        "ttt": "git"
                    },{
                        "id": "/%E4%BB%A3%E7%A0%81/2020/01/19/git.html",
                        "name": "Git 操作使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E4%BB%A3%E7%A0%81/2020/01/19/git.html",
                        "ttt": "github"
                    },{
                        "id": "/%E4%BB%A3%E7%A0%81/2020/01/19/git.html",
                        "name": "Git 操作使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E4%BB%A3%E7%A0%81/2020/01/19/git.html",
                        "ttt": "gitlab"
                    },{
                        "id": "/%E4%BB%A3%E7%A0%81/2020/01/19/git.html",
                        "name": "Git 操作使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E4%BB%A3%E7%A0%81/2020/01/19/git.html",
                        "ttt": "vcs"
                    },{
                        "id": "/tools/2020/01/20/tesseract.html",
                        "name": "Tesseract 使用记录",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2020/01/20/tesseract.html",
                        "ttt": "OCR"
                    },{
                        "id": "/tools/2020/01/20/tesseract.html",
                        "name": "Tesseract 使用记录",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2020/01/20/tesseract.html",
                        "ttt": "tesseract"
                    },{
                        "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/21/Flink-All-in-one.html",
                        "name": "Flink All in one",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/01/21/Flink-All-in-one.html",
                        "ttt": "flink"
                    },{
                        "id": "/inmgr/2020/02/14/the-future-of-inmgr.html",
                        "name": "接口平台的反思与发展",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/inmgr/2020/02/14/the-future-of-inmgr.html",
                        "ttt": "inmgr"
                    },{
                        "id": "/inmgr/2020/02/14/the-future-of-inmgr.html",
                        "name": "接口平台的反思与发展",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/inmgr/2020/02/14/the-future-of-inmgr.html",
                        "ttt": "api"
                    },{
                        "id": "/personal/2020/02/16/fire.html",
                        "name": "FIRE",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/personal/2020/02/16/fire.html",
                        "ttt": "个人理财"
                    },{
                        "id": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/02/17/Once-Upon-a-Time-in-Hollywood.html",
                        "name": "好莱坞往事",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/02/17/Once-Upon-a-Time-in-Hollywood.html",
                        "ttt": "电影"
                    },{
                        "id": "/personal/2020/03/07/the-art-of-talk.html",
                        "name": "说话的艺术",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/personal/2020/03/07/the-art-of-talk.html",
                        "ttt": "为人处事"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/03/apm.html",
                        "name": "APM搭建使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/03/apm.html",
                        "ttt": "pinpoint"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/03/apm.html",
                        "name": "APM搭建使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/03/apm.html",
                        "ttt": "APM"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/03/apm.html",
                        "name": "APM搭建使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/03/apm.html",
                        "ttt": "skywalking"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/11/ci.html",
                        "name": "Jenkins 环境搭建",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/11/ci.html",
                        "ttt": "Jenkins"
                    },{
                        "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/04/12/hadoop.html",
                        "name": "Hadoop 搭建",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/04/12/hadoop.html",
                        "ttt": "bigdata"
                    },{
                        "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/04/12/hadoop.html",
                        "name": "Hadoop 搭建",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/04/12/hadoop.html",
                        "ttt": "hadoop"
                    },{
                        "id": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/04/19/eggplant.html",
                        "name": "风味茄子",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/04/19/eggplant.html",
                        "ttt": "茄子"
                    },{
                        "id": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/04/19/eggplant.html",
                        "name": "风味茄子",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%90%83%E5%96%9D%E7%8E%A9%E4%B9%90/2020/04/19/eggplant.html",
                        "ttt": "eggplant"
                    },{
                        "id": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/19/ssh.html",
                        "name": "SSH免密登录",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%BC%80%E5%8F%91%E8%BF%90%E7%BB%B4/2020/04/19/ssh.html",
                        "ttt": "ssh"
                    },{
                        "id": "/linux/2020/05/06/test-all-in-one.html",
                        "name": "测试工具使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/linux/2020/05/06/test-all-in-one.html",
                        "ttt": "test"
                    },{
                        "id": "/linux/2020/05/06/arthas.html",
                        "name": "Arthas使用教程",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/linux/2020/05/06/arthas.html",
                        "ttt": "test"
                    },{
                        "id": "/linux/2020/05/06/test-all-in-one.html",
                        "name": "测试工具使用",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/linux/2020/05/06/test-all-in-one.html",
                        "ttt": "测试"
                    },{
                        "id": "/linux/2020/05/06/arthas.html",
                        "name": "Arthas使用教程",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/linux/2020/05/06/arthas.html",
                        "ttt": "测试"
                    },{
                        "id": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2020/06/01/ddp.html",
                        "name": "设计模式-访问者模式",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2020/06/01/ddp.html",
                        "ttt": "ddp"
                    },{
                        "id": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2020/06/01/ddp.html",
                        "name": "设计模式-访问者模式",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F/2020/06/01/ddp.html",
                        "ttt": "访问者模式"
                    },{
                        "id": "/%E5%B7%A5%E5%85%B7/2020/06/17/sublime.html",
                        "name": "Sublime 快捷键",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%B7%A5%E5%85%B7/2020/06/17/sublime.html",
                        "ttt": "sublime"
                    },{
                        "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/11/17/es.html",
                        "name": "ES数据操作",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/11/17/es.html",
                        "ttt": "es"
                    },{
                        "id": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/11/17/es.html",
                        "name": "ES数据操作",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/%E5%A4%A7%E6%95%B0%E6%8D%AE/2020/11/17/es.html",
                        "ttt": "elasticsearch"
                    },{
                        "id": "/tools/2021/12/05/ddns.html",
                        "name": "ddns",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2021/12/05/ddns.html",
                        "ttt": "工具"
                    },{
                        "id": "/tools/2021/12/03/nacos.html",
                        "name": "nacos",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2021/12/03/nacos.html",
                        "ttt": "工具"
                    },{
                        "id": "/tools/2021/12/01/docsify.html",
                        "name": "docsify打包docker镜像",
                        "value": "文章",
                        "category": "文章",
                        "label": {"show": true},
                        "symbolSize": 20,
                        "symbol": 'circle',
                        "x": randomX(),
                        "y": randomY(),
                        "url": "/tools/2021/12/01/docsify.html",
                        "ttt": "工具"
                    },].filter(function (item) {
                    return item.ttt === tag;
            });
            nodes = nodes_tag.concat(nodes_post);
        }

        return {
            "categories": categories,
            "links": links,
            "nodes": nodes
        }
    }
      // 使用配置项设置图表
      myChart.setOption(option);
    };

    // 使用 Vue 3 的生命周期钩子 onMounted 来初始化图表
    onMounted(() => {
      initECharts();
    });

    return {
      echartsContainer, // 返回 ref 以供模板使用
    };
  },
};
</script>
  
  <style scoped>
/* 样式可以根据需要进行调整 */
</style>
  