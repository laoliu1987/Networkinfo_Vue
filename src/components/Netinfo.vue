<template>
    <div class="main_welcome">
      <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/home' }">主机信息</el-breadcrumb-item>
        <el-breadcrumb-item :to="{path:'/netinfo'}">网络信息</el-breadcrumb-item>
      </el-breadcrumb>
      <el-card style="height: 750px">
        <el-card style="width: 700px; height:400px;float: left;margin-right: 30px">
          <div slot="header" class="clearfix">
            <i class="el-icon-monitor" style="margin-right: 10px"></i>
            <span>{{localData['LocalName']}}</span>
          </div>
          <div style="font-size: 10px">
          <div style="margin-top: 15px"><span style="width: 100px">主机名称</span><i class="el-icon-arrow-right" style="margin-left: 50px;margin-right: 50px"></i>{{localData['LocalName']}}</div>
          <div style="margin-top: 15px"><span style="width: 100px">本机IPv4地址</span><i class="el-icon-arrow-right" style="margin-left: 25px;margin-right: 50px"></i>{{localData['ipv4_address']}}</div>
          <div style="margin-top: 15px"><span style="width: 100px">本机IPv6地址</span><i class="el-icon-arrow-right" style="margin-left: 25px;margin-right: 50px"></i>{{localData['ipv6_address']}}</div>
          <div style="margin-top: 15px"><span style="width: 100px">DHCP服务器</span><i class="el-icon-arrow-right" style="margin-left: 27px;margin-right: 50px"></i>{{localData['dhcp_server']}}</div>
            <div style="margin-top: 15px"><span style="width: 100px">当前网卡设备</span><i class="el-icon-arrow-right" style="margin-left: 24px;margin-right: 50px"></i>{{localData['Device']}}</div>
          <div style="margin-top: 15px"><span style="width: 100px">MAC地址</span><i class="el-icon-arrow-right" style="margin-left: 44px;margin-right: 50px;margin-bottom: 68px"></i>{{localData['HardwareAddress']}}</div>
          <hr>
          <div style="margin-top: 15px"><span style="width: 100px">操作系统</span><i class="el-icon-arrow-right" style="margin-left: 50px;margin-right: 50px"></i>{{sysData['system']}}</div>
          </div>
        </el-card>
        <el-card style="width: 700px; height:400px;float: left">
          <div slot="header" class="clearfix">
            <i class="el-icon-connection" style="margin-right: 10px"></i>
            <span>{{netData['ip']}}</span>
          </div>
            <div style="font-size: 10px">
              <div style="margin-top: 15px"><span style="width: 100px"><i class="el-icon-connection" style="margin-right: 10px"></i>公网IP地址</span><i class="el-icon-arrow-right" style="margin-left: 50px;margin-right: 50px"></i>{{netData['ip']}}</div>
              <div style="margin-top: 15px"><span style="width: 100px"><i class="el-icon-sold-out" style="margin-right: 10px"></i>运营商</span><i class="el-icon-arrow-right" style="margin-left: 72px;margin-right: 50px"></i>{{netData['country']}}{{netData['isp']}}</div>
              <div style="margin-top: 15px"><span style="width: 100px"><i class="el-icon-location-outline" style="margin-right: 10px"></i>所属地区</span><i class="el-icon-arrow-right" style="margin-left: 60px;margin-right: 50px"></i>{{netData['area']}}</div>
              <div style="margin-top: 15px"><span style="width: 100px"><i class="el-icon-location-outline" style="margin-right: 10px"></i>国家代码</span><i class="el-icon-arrow-right" style="margin-left: 60px;margin-right: 50px"></i>{{netData['country_id']}}</div>
              <div style="margin-top: 15px"><span style="width: 100px"><i class="el-icon-place" style="margin-right: 10px"></i>所在国家/地区</span><i class="el-icon-arrow-right" style="margin-left: 30px;margin-right: 50px"></i>{{netData['country']}}</div>
              <div style="margin-top: 15px"><span style="width: 100px"><i class="el-icon-map-location" style="margin-right: 10px"></i>所在省/市/县/区</span><i class="el-icon-arrow-right" style="margin-left: 20px;margin-right: 50px;margin-bottom: 68px"></i>{{netData['region']}}{{netData['city']}}</div>
              <hr>
              <div style="margin-top: 15px"><span style="width: 100px">长整形IP地址</span><i class="el-icon-arrow-right" style="margin-left: 36px;margin-right: 50px"></i>{{netData['long_ip']}}</div>
            </div>
        </el-card>
        <el-card style="width: 170px;height: 230px; margin-top: 30px;float: left">
          <div slot="header" class="clearfix">
            <i class="el-icon-cpu" style="margin-right: 10px"></i>
            <span>内存使用率</span>
          </div>
          <el-progress  v-on="sysData" type="dashboard" :percentage="sysData['rate']" :color="colors"></el-progress>
        </el-card>
        <el-card style="width: 500px; height: 230px;margin-top: 30px;margin-left: 30px;float: left">
          <div slot="header" class="clearfix">
            <i class="el-icon-connection" style="margin-right: 10px"></i>
            <span>磁盘空间</span>
            <el-progress v-on="diskData" :percentage="diskData['c_rate']" :color="colors_1"></el-progress>
          </div>
          <div style="font-size: 10px">C:\<el-progress v-on="diskData" :percentage="diskData['c_rate']" :color="colors_1"></el-progress>剩余{{diskData['c_left']}}G</div>
        </el-card>

        <el-card style="width: 500px; height: 230px;margin-top: 30px;margin-left: 30px;float: left">
          <div slot="header" class="clearfix">
            <i class="el-icon-chat-square" style="margin-right: 10px"></i>
            <span>公告</span>
          </div>
          <div style="font-size: 10px">
            <div><span style="width: 100px"><i class="el-icon-chat-dot-square" style="margin-right: 10px"></i>2021.1.2 23:17</span><i class="el-icon-arrow-right" style="margin-left: 20px;margin-right: 20px"></i>项目总体完成</div>
          </div>
        </el-card>
      </el-card>
    </div>
</template>
<style lang="less" scoped>

</style>
<script>
export default {
    data(){
      return{
        netData:[],
        sysData:[],
        localData:[],
        diskData:[],
        colors:[
          {color:'#32CD32',percentage:50},
          {color:'#3278cd',percentage:80},
          {color:'#FF0000',percentage:100},
        ],
        colors_1:[
          {color:'#32CD32',percentage:20},
          {color:'#3278cd',percentage:80},
          {color:'#FF0000',percentage:100},
        ],
        timer:'',
        value:0
      };
    },
    created() {
      this.openFullScreen2()
      this.getNetInfo()
      this.getSysInfo()
      this.getLocalInfo()
      this.getDiskInfo()
    },
  methods:{
      async getNetInfo(){
        const {data:res} = await  this.$http.get('/netInfo')
        this.netData=res.data;
        console.log(res);
      },
      async getSysInfo(){
        const {data:res} = await this.$http.get('/getSysInfo')
        this.sysData=res;
        console.log(res)
      },
      async getLocalInfo(){
        const{data:res} =await this.$http.get('/info')
        this.localData=res.data;
        console.log(res)
      },
      async getDiskInfo(){
        const{data:res} =await this.$http.get('/getDisk')
        this.diskData=res;
        console.log(res)
      },
      openFullScreen2() {
        const loading = this.$loading({
          lock: true,
          text: '加载中...',
          spinner: 'el-icon-loading',
          background: 'rgba(0, 0, 0, 0.7)'
        });
        setTimeout(() => {
          loading.close();
        }, 2000);
      }
    },
  mounted() {
      this.timer = setInterval(this.getSysInfo,5000);
  },
  beforeDestroy() {
      clearInterval(this.timer);
  }
}
</script>