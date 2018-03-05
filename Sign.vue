<template>
  <div class="container">
    <div id="canvasBox" :style="getHorizontalStyle" v-show="!showBox">
      <div class="greet">
        <span>{{msg}}</span>
        <input type="button" value="重写" @touchstart="clear" @mousedown="clear"/>
        <!-- <input type="button" value="生成png图片" @touchstart="savePNG" @mousedown="savePNG"/> -->
        <input type="button" value="确定" @touchstart="upload" />
      </div>
      <canvas></canvas>
    </div>
    <div class="image-box" v-show="showBox">
      <header>
        请长按图片并保存至本地后发送好友
        <input type="button" value="返回" @click="showBox = false"/>
      </header>
      <img :src="signImage">
    </div>
  </div>
</template>

<script>
import Draw from '../utils/draw';
import units from '../tools/units';
import cookie from '../tools/cookie';
export default {
  name: 'canvas',
  data() {
    return {
      msg: '请在下方空白处签名',
      degree: 90,
      signImage: null,
      showBox: false,
    };
  },
  components: {
    Draw,
  },
  beforeCreate() {
    document.title = '手写签名';
  },
  mounted() {
    this.canvasBox = document.getElementById('canvasBox');
    this.initCanvas();
  },
  computed: {
    getHorizontalStyle() {
      const d = document;
      const w = window.innerWidth || d.documentElement.clientWidth || d.body.clientWidth;
      const h = window.innerHeight || d.documentElement.clientHeight || d.body.clientHeight;
      let length = (h - w) / 2;
      let width = w;
      let height = h;

      switch (this.degree) {
        case -90:
          length = -length;
        case 90:
          width = h;
          height = w;
          break;
        default:
          length = 0;
      }
      if (this.canvasBox) {
        this.canvasBox.removeChild(document.querySelector('canvas'));
        this.canvasBox.appendChild(document.createElement('canvas'));
        setTimeout(() => {
          this.initCanvas();
        }, 200);
      }
      return {
        transform: `rotate(${this.degree}deg) translate(${length}px,${length}px)`,
        width: `${width}px`,
        height: `${height}px`,
        transformOrigin: 'center center',
      };
    },
  },
  methods: {
    initCanvas() {
      const canvas = document.querySelector('canvas');
      this.draw = new Draw(canvas, -this.degree);
    },
    clear() {
      this.draw.clear();
    },
    download() {
      this.draw.downloadPNGImage(this.draw.getPNGImage());
    },
    savePNG() {
      this.signImage = this.draw.getPNGImage();
      this.showBox = true;
    },
    upload() {
        // alert(111);
        // console.log(1111);
      const image = this.draw.getPNGImage();
      // console.log(image);
      const blob = this.draw.dataURLtoBlob(image);
      // console.log(blob);
       var uid = cookie.get('user_id');
      const url = 'http://h5.wwcrpt.com/index.php/index/toolure/upload_contract?u='+uid;
      const successCallback = (response) => {
        console.log(response);
      };
      const failureCallback = (error) => {
        // alert(1111);
        cookie.set('c_status', 1);
        let that = this;
        this.$http.post(units.host('findcar'), units.params(JSON.parse(cookie.get('findCarForm')))).then(function (res) {
                    if (res.data.code > 0) {
                        layer.msg(res.data.info, 2, function () {
                            cookie.del('findCarForm');
                            cookie.del('cards');
                            if(that.zl == 'send'){
                                location.href = '#/server/terrace?id='+res.data.msg
                            }else{
                                that.href('pay?type=2&order=' + res.data.code)
                            }
                        })
                    }
                });
        // location.href='#/contracted';
      };
      this.draw.upload(blob, url, successCallback, failureCallback);
    },
  },
};


</script>

<style>
.container {
  width: 100%;
  height: 100%;
}
#canvasBox {
  display: flex;
  flex-direction: column;
  height: 100%;
}
.greet {
  padding: 20px;
  font-size: 20px;
  user-select: none;
}
input {
  font-size: 20px;
}
.greet select {
  font-size: 18px;
}
canvas {
  flex: 1;
  cursor: crosshair;
  border:2px dashed lightgray;
}
.image-box {
  width: 100%;
  height: 100%;
}
.image-box header{
  font-size: 18px;
}
.image-box img {
  max-width: 80%;
  max-height: 80%;
  margin-top: 50px;
  border: 1px solid gray;
}
</style>

<!--  <template>
  <div id="canvasBox" :style="getHorizontalStyle">
    <div class="greet">
      <span>{{msg}}</span>
      <a @touchstart="clear" @mousedown="clear">清屏</a>
      <a @touchstart="download" @mousedown="download">下载</a>
      <select v-model="degree">
        <option v-for="item in scope" :value="item.value">{{item.title}}</option>
      </select>
    </div>
    <canvas></canvas>
  </div>
</template>

<script>
import Draw from '../utils/draw';

export default {
  name: 'canvas',
  data() {
    return {
      msg: 'Just use canvas to draw',
      degree: 0, // 屏幕整体旋转的角度, 可取 -90,90,180等值
      scope: [
        {
          value: 0,
          title: '正常',
        },
        {
          value: 90,
          title: '顺时针旋转90°',
        },
        {
          value: 180,
          title: '顺时针旋转180°',
        },
        {
          value: -90,
          title: '逆时针旋转90°',
        },
      ],
    };
  },
  components: {
    Draw,
  },
  mounted() {
    this.canvasBox = document.getElementById('canvasBox');
    this.initCanvas();
  },
  computed: {
    getHorizontalStyle() {
      const d = document;
      const w = window.innerWidth || d.documentElement.clientWidth || d.body.clientWidth;
      const h = window.innerHeight || d.documentElement.clientHeight || d.body.clientHeight;
      let length = (h - w) / 2;
      let width = w;
      let height = h;

      switch (this.degree) {
        case -90:
          length = -length;
        case 90:
          width = h;
          height = w;
          break;
        default:
          length = 0;
      }
      if (this.canvasBox) {
        this.canvasBox.removeChild(document.querySelector('canvas'));
        this.canvasBox.appendChild(document.createElement('canvas'));
        setTimeout(() => {
          this.initCanvas();
        }, 200);
      }
      return {
        transform: `rotate(${this.degree}deg) translate(${length}px,${length}px)`,
        width: `${width}px`,
        height: `${height}px`,
        transformOrigin: 'center center',
      };
    },
  },
  methods: {
    initCanvas() {
      const canvas = document.querySelector('canvas');
      this.draw = new Draw(canvas, -this.degree);
    },
    clear() {
      this.draw.clear();
    },
    download() {
      this.draw.downloadPNGImage(this.draw.getPNGImage());
    },
    upload() {
      const image = this.draw.getPNGImage();
      const blob = this.draw.dataURLtoBlob(image);

      const url = '';
      const successCallback = (response) => {
        console.log(response);
      };
      const failureCallback = (error) => {
        console.log(error);
      };
      this.draw.upload(blob, url, successCallback, failureCallback);
    },
  },
};


</script>

<style>
#canvasBox {
  display: flex;
  flex-direction: column;
  height: 100%;
}
.greet {
  padding: 20px;
  font-size: 20px;
  user-select: none;
}
.greet a {
  cursor: pointer;
}
.greet select {
  font-size: 18px;
}
canvas {
  flex: 1;
  cursor: crosshair;
}
</style>
 -->