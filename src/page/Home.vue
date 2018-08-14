<template>
  <div>
      <Nav/>
      <div class="first-screen">
        <!-- <img src="../assets/first_screen.jpg" alt=""> -->
        <!-- <img src="../assets/home/first-screen.webp" alt=""> -->
      </div>
      <div class="quick_check">
        <div class="container">
            <div class="col-lg-7 wrap">
				<div class="title">我要买车 ></div>
				<div class="link-group">
					<div>
						<div class="col-lg-1" v-for="(row,index) in brand_list" :key="index">
							<router-link class="tag" :to="'/search/?brand_id=' + row.id" >
								{{row.name}}
							</router-link>
						</div>
					</div>
					<div>
						<div class="col-lg-1">
							<span class="tag">3万以下</span>
						</div>
						<div class="col-lg-1">
							<span class="tag">3-5万</span>
						</div>
						<div class="col-lg-1">
							<span class="tag">5-10万</span>
						</div>
						<div class="col-lg-1">
							<span class="tag">10-15万</span>
						</div>
						<div class="col-lg-1">
							<span class="tag">15-20万</span>
						</div>
						<div class="col-lg-1">
							<span class="tag">20-30万</span>
						</div>
					</div>
					<div>
						<div class="col-lg-1">
							<span class="tag">降价车</span>
						</div>
						<div class="col-lg-1">
							<span class="tag">准新车</span>
						</div>
						<div class="col-lg-1">
							<span class="tag">紧凑车型</span>
						</div>
						<div class="col-lg-1">
							<span class="tag">急售车</span>
						</div>
						<div class="col-lg-1">
							<span class="tag">中大车型</span>
						</div>
						<div class="col-lg-1">
							<span class="tag">豪华车型</span>
						</div>
					</div>
				</div>
				<div>
					<SearchBar/>
				</div>
            </div>
          <div class="col-lg-4 wrap">
            <div class="title">我要卖车 ></div>
            <div>
				<input placeholder="请输入手机号" class="sell-input">
			</div>
			<div>
				<span>
					<button class="btn-fat">我要买车</button>
					<button class="btn-fat">我要卖车</button>
				</span>
			</div>
          </div>

        </div>
      </div>
      <div class="chanle-wrap">
        <div class="container">
			<div class="title">
				<span class="main">保卖车</span>
				<span class="desc">限时出售 | 性价比高</span>
			</div>
			<div class="card-group">
				<div class="col-lg-2" style="width:19.4444%">
					<div class="col-card c1">
						<div class="c1-title">仃仃保卖车</div>
						<div class="c1-desc">限时出售 | 高性价比</div>
					</div>
					<!-- <img src="../assets/224x344.png" alt=""> -->
				</div>
				<div class="col-lg-2" style="width:19.4444%">
          			<div class="col-card c2">
						<img src="../assets/home/card-1.png" alt="">
						<div class="c2-title">选你所爱</div> 
						<div class="c2-desc">3年内准新车</div> 
					</div>
					<!-- <img src="../assets/224x344.png" alt=""> -->
				</div>
				<div class="col-lg-5 y-img">
					<div>
            			<div class="row-card c1">
							<img src="../assets/home/card-1.png" alt="">
							<div class="c1-title">选你所爱</div> 
							<div class="c1-desc">3年内准新车</div> 
						</div>
					</div>
					<div>
            			 <div class="row-card c2">
							<img src="../assets/home/card-1.png" alt="">
							<div class="c2-title">选你所爱</div> 
							<div class="c2-desc">3年内准新车</div>
						 </div>
					</div>
				</div>
				<div class="col-lg-2" style="width:19.4444%">
          			<div class="col-card c2">
						<img src="../assets/home/card-1.png" alt="">
						<div class="c2-title">选你所爱</div> 
						<div class="c2-desc">3年内准新车</div> 
					</div>
					<!-- <img src="../assets/224x344.png" alt=""> -->
				</div>
			</div>
        </div>
      </div>
      <!-- 车列表 导航 -->
      <div class="vehicle-nav">
        <div class="container">
          <div @click="read_main('on_sale')" class="col-lg-2 item">
            特价好车
          </div>
          <div @click="read_main('under_5')" class="col-lg-2 item">
            5万以下
          </div>
          <div @click="read_main('between_5_10')" class="col-lg-2 item">
            5-10万
          </div>
          <div @click="read_main('suv')" class="col-lg-2 item">
            超值SUV
          </div>
          <div @click="read_main('urgent')" class="col-lg-2 item">
            急售降价车
          </div>
          <div class="col-lg-2 item">
            更多
          </div>
        </div>
      </div>
      <!-- 车 列表 -->
      <div class="vehicle-list">
        <div class="container">
          <div class="col-lg-3" v-for="(row,index) in main_list" :key="index">
            <div class="card" >
                <div class="thumbnail">
                  <img :src="row.preview[0].url" alt="">
                </div>
                <div class="detail">
                  <div class="title">{{row.title}}</div>
                  <div class="desc">{{row.birth_day|only_day}} / {{row.consumed_distance}}万公里</div>
                  <div class="other">
                    <div class="col-lg-8">
                      <span class="price">{{row.price}}万</span>
                      <span class="f-pay">首付{{row.price }}万</span>
                    </div>
                    <div class="col-lg-4 right">
                      <router-link :to="'/detail/' + row.id" class="link">详情</router-link>
                    </div>
                  </div>
                </div>
            </div>
          </div>
        </div>
      </div>
	  <Footer/>
  </div>
</template>

<script>
import '../css/vehicle.css';
import Nav from "../components/Nav.vue";
import SearchBar from "../components/SearchBar";
import Footer from "../components/Footer";
import api from "../lib/api";
import Reader from "../mixin/Reader";

export default {
  components: { Nav, SearchBar ,Footer},
  mixins:[Reader],
  data() {
    return {
      list: [],
      main_list:[],
      model: "vehicle",
	  design:[],
	  brand_list:[],
      
    };
  },
  methods: {
    find_design(name){
      api('design/search',{or:{name:name}})
        .then(r=>{
          this.design[name] = r.data[0];
          console.log('design r.data',r.data);
          
        })
    },
    read_main(type){
      let condition = {};
      switch (type){
        case 'on_sale':
          condition = {
            where:{
              and:{
                on_sale:true,
              }
            }
          };
          break;
        case 'under_5':
          condition = {
            where:{
              or:[
                ['price','<',5],
              ]
            }
          };
          break;
        case 'between_5_10':
          condition = {
            where:{
              and:[
                ['price','>=',5],
                ['price','<',10],
              ]
            }
          };
          break;
        case 'SUV':
          condition = {
            where:{
              and:{
                design_id:this.design_id.SUV.id,
              }
            }
          };
          break;
        case 'urgent':
          let date = new Date;
          date.setDate(date.getDate() + 30);
          date = date.toISOString().split('T')[0];
          condition = {query:`where('deadline' <= ${date})`};
          break;
      }
      api('vehicle/search',condition)
        .then(r=>{
          console.log("this['main_list']",this['main_list']);
          
          this['main_list'] = r.data;
        })
	},
	read_brand(){
		api('brand/read',{
			where:{
				is_recommend:true,
			}
		}).then(r=>{
			this.brand_list= r.data;
		})
	}
  },
  mounted() {
    this.read_brand();
    this.read_main('on_sale')
    this.find_design('SUV');

  }
};
</script>
<style scoped>
.first-screen {
  background-image: url(../assets/first_screen.jpg);
  background-repeat: no-repeat;
  background-position: top;
  background-size: cover;
  -webkit-background-size: cover;
  -o-background-size: cover;
  -moz-background-size: cover;
  min-height: 420px;
  opacity: 0.8;
}

.quick_check {
  padding: 20px;
}

.quick_check .container {
  background: #fff;
  padding: 20px 10px;
  border: 1px solid rgba(0, 0, 0, 0.06);
  box-shadow: 3px 4px 10px rgba(0, 0, 0, 0.04);
  border-radius: 5px;
}

.quick_check .container .wrap {
  padding: 0px 20px;
}

 .quick_check .container .wrap .title{
  color: #0b5a81;
  font-size: 1.1rem;
  /* margin-lesft: 15px; */
  padding: 10px 0;
}

.quick_check .wrap .sell-input{
	width: 100%;
	margin: 20px 0;
	border-radius: 2px;
	background-color:rgba(0, 0, 0, 0.04);
}
.quick_check .wrap .btn-fat{
	margin: 0 5px;
	border-radius: 2px;
	color: #fff;
	opacity: .9;
	
}
.quick_check .wrap .btn-fat:first-child{
	background: #0B5A81;
}
.quick_check .wrap .btn-fat:last-child{
	background: #E08109;
}
.tip {
  font-size: 0.8rem;
}
.link-group{
	margin-left: -13px;
}
.link-group > * {
	padding: 8px 0px;
	font-size: 1rem;
}

.link-group .col-lg-1{
	text-align: center;
	width: 14.28%;
}
.link-group input {
  width: 45%;
}

.link-group input,
.link-group button {
  padding: 10px;
  vertical-align: top;
}

.link-group button {
  border-left: 0;
}

.link-group button:hover {
  background: #fd521d;
}
.chanle-wrap {
	margin: 30px 0;
}
.chanle-wrap .title{
	margin: 16px 0;
}
.chanle-wrap .card-group {
  margin-right: -17px;
}
.chanle-wrap .card-group .col-card{
  height: 300px;
  width: 197px;
  background: #fff;
	padding: 0 8px;
}
.chanle-wrap .card-group .row-card{
  width: 440px;
  height: 144px;
  background: #fff;
}
.chanle-wrap .card-group .y-img>* {
	padding-bottom: 10px;
}
.chanle-wrap .title .main{
	font-size: 1.1rem;
	font-weight: 600;
	padding: 5px;
	padding-right: 20px;
}
.chanle-wrap .title .desc {
  font-size: 0.8rem;
  color: #a8abae;
}
.chanle-wrap .col-card.c1,
.chanle-wrap .col-card.c2,
.chanle-wrap .row-card.c1,
.chanle-wrap .row-card.c2{
  position: relative;
}
.chanle-wrap .col-card.c1{
	background: #0B5A81;
}
.chanle-wrap .col-card.c1 .c1-title{
  position: absolute;
  top:15%;
  right: 21%;
  font-size: 1.5rem;
  font-weight: 700;
  color: #fff;
  letter-spacing: 0.15rem;
}
.chanle-wrap .col-card.c1 .c1-desc{
	position: absolute;
	top: 32%;
	right: 22%;
	font-size: 0.9rem;
	color: #a8abae;
}
.chanle-wrap .col-card.c2 .c2-title{
	position: absolute;
	font-size: 1rem;
	right: 35%;
	top:55%;
}
.chanle-wrap .col-card.c2 .c2-desc {
	position: absolute;
	font-size: 1.1ren;
	top: 67%;
	right: 28%;
	color: red;
}
.chanle-wrap .row-card.c1 .c1-title,
.chanle-wrap .row-card.c2 .c2-title {
	position: absolute;
	font-size: 1rem;
	top:25%;
	right: 20%;
}
.chanle-wrap .row-card.c1 .c1-desc, 
.chanle-wrap .row-card.c2 .c2-desc
{
	position: absolute;
	font-size: 1.1ren;
	top: 46%;
	right: 18%;
	color: red;
}
.chanle-wrap .col-card.c2 img{
	position: relative;
	top:19%;
}
.chanle-wrap .row-card.c1 img,
.chanle-wrap .row-card.c2 img{
	position: relative;
	width: 230px;
	height: 90px;
	top: 15%;
	left: 2%;
}

.vehicle-nav .item {
  padding: 10px;
  font-size: 1.6rem;
  text-align: center;
  border: 1px solid rgba(0, 0, 0, 0.06);
}

.vehicle-nav .item:hover {
  background: #0b5a81;
  color: #fff;
}
a {
  color:#000;
}
</style>