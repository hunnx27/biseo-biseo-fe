<template>
  <!-- Wrap START -->
  <div class="home">
    <!-- section1 -->
    <div @click="detailCounsel(item.id)" v-if="Object.keys(item).length>0">
      <div
        class="lighten-5 pa-0 ma-0 block"
        :style="{backgroundImage: `url('/resources/images/new_list_top.jpg')`}"
      >
        <v-row no-gutters class="px-4 pt-4">
          <v-col class="text-left">
            <v-chip color="white" outlined v-if="item.counselStateCode=='R'">{{item.counselStateName}}</v-chip>
            <v-chip color="yellow" outlined v-else>{{item.counselStateName}}</v-chip>
          </v-col>
          <v-col class="text-right">
            <v-chip color="red" text-color="white" v-if="item.isMine">내질문</v-chip>
            <v-chip color="white" outlined v-else>{{item.gubnName}}</v-chip>
          </v-col>
        </v-row>
        <v-row class="text-center pa-0 ma-0" style="width: 100%;position:relative">
          <v-col class="py-0 px-3">
            <div class="px-9">
              <v-row no-gutters>
                <v-col
                  class="py-3 text-h7"
                  style="color: #039be5; font-weight: bolder"
                >
                  {{item.inputTag}}
                </v-col>
              </v-row>
              <v-row no-gutters>
                <v-col class="pa-2 white--text counsel-txt" v-html="item.txt.replaceAll('\n','<br/>')">
                  
                </v-col>
              </v-row>
            </div>
          </v-col>
        </v-row>
      </div>
      <div class="ma-0 pa-0">
        <v-row no-gutters class="pa-3" style="background-color: #000000cc">
          <v-col class="text-left white--text"> {{item.createDate}} </v-col>
          <v-col class="text-right white--text">
            답변({{item.reportCnt}}) 포인트(답변10/채택100)
          </v-col>
        </v-row>
      </div>
    </div>
    <LoadingItem isLoading="true" v-else></LoadingItem>

    <!-- section2 -->
    <div class="lighten-5 text-center">
      <v-row no-gutters class="pa-3">
        <v-col>
          <v-chip color="" outlined label>넘나 고민되는 것</v-chip>
        </v-col>
      </v-row>
      <v-row no-gutters class="pa-1">
        <v-col class="text-h5"> 마음 속 이야기 </v-col>
      </v-row>
    </div>

    <v-divider></v-divider>

    <!-- section3 -->
    <div class="lighten-5 text-center">
      <v-row no-gutters>
        <v-col style="padding: 13px 0;" @click="searchCounselByTag('고민')"><v-icon style="margin-top: -3px;font-size: 21px;color: #444;">mdi-pound</v-icon>고민</v-col>
        <v-col style="padding: 13px 0;" @click="searchCounselByTag('휴가')"><v-icon style="margin-top: -3px;font-size: 21px;color: #444;">mdi-pound</v-icon>휴가</v-col>
        <v-col style="padding: 13px 0;" @click="searchCounselByTag('호봉')"><v-icon style="margin-top: -3px;font-size: 21px;color: #444;">mdi-pound</v-icon>호봉</v-col>
      </v-row>
      <v-row no-gutters>
        <v-col style="padding: 13px 0;" @click="searchCounselByTag('임용')"><v-icon style="margin-top: -3px;font-size: 21px;color: #444;">mdi-pound</v-icon>임용</v-col>
        <v-col style="padding: 13px 0;" @click="searchCounselByTag('보조')"><v-icon style="margin-top: -3px;font-size: 21px;color: #444;">mdi-pound</v-icon>보조</v-col>
        <v-col style="padding: 13px 0;" @click="searchCounselByTag('평가인증')"><v-icon style="margin-top: -3px;font-size: 21px;color: #444;">mdi-pound</v-icon>평가인증</v-col>
      </v-row>
    </div>

    <!-- section4 리스트 반복 -->
    <div v-for="(item, index) in list" :key="item.id" @click="detailCounsel(item.id)">
      <div
        class="lighten-5 pa-0 ma-0 block"
        :style="{backgroundImage: `url('${getBackgroundUrl(index)}')`}"
      >
        <v-row no-gutters class="px-4 pt-4">
          <v-col class="text-left">
            <v-chip color="white" outlined v-if="item.counselStateCode=='R'">{{item.counselStateName}}</v-chip>
            <v-chip color="yellow" outlined v-else>{{item.counselStateName}}</v-chip>
          </v-col>
          <v-col class="text-right">
            <v-chip color="red" text-color="white" v-if="item.isMine">내질문</v-chip>
            <v-chip color="white" outlined v-else>{{item.gubnName}}</v-chip>
          </v-col>
        </v-row>
        <v-row class="text-center pa-0 ma-0" style="width: 100%;position:relative">
          <v-col class="py-0 px-3">
            <div class="px-9">
              <v-row no-gutters>
                <v-col
                  class="py-3 text-h7 white--text"
                  style="color: #039be5; font-weight: bolder"
                >
                  {{item.inputTag}}
                </v-col>
              </v-row>
              <v-row no-gutters>
                <v-col class="pa-2 white--text counsel-txt" v-html="item.txt.replaceAll('\n','<br/>')">
                  
                </v-col>
              </v-row>
            </div>
          </v-col>
        </v-row>
      </div>
      <div class="ma-0 pa-0">
        <v-row no-gutters class="pa-3" style="background-color: #000000cc">
          <v-col class="text-left white--text"> {{item.createDate}} </v-col>
          <v-col class="text-right white--text">
            답변({{item.reportCnt}}) 포인트(답변10/채택100)
          </v-col>
        </v-row>
      </div>
    </div>
    <LoadingItem :isLoading="isLoading"></LoadingItem>
  </div>
  <!-- Wrap END -->
</template>

<script>
import counselApi from "@/api/counsel";
import LoadingItem from "@/components/common/LoadingItem.vue"
export default {
  name: "HomeItem",
  components: {LoadingItem},
  data() {
    return {
      item: {},
      list: [],
      backgroundUrls: [
        'https://appstage.oneandzip.com/test/new_list00.jpg',
        'https://appstage.oneandzip.com/test/new_list01.jpg',
        'https://appstage.oneandzip.com/test/new_list02.jpg',
        'https://appstage.oneandzip.com/test/new_list03.jpg',
        'https://appstage.oneandzip.com/test/new_list04.jpg',
        'https://appstage.oneandzip.com/test/new_list05.jpg',
        'https://appstage.oneandzip.com/test/new_list06.jpg',
        'https://appstage.oneandzip.com/test/new_list07.jpg',
      ],
      curpage:-1,
      size:2,
      isLoading: false,
      lastScrollY: 0
    };
  },
  methods: {
    searchAllList(){
      this.isLoading=true;
      const reqpage = this.curpage+1;
      console.log('START searchAllList ' + `req:${reqpage}, cur:${this.curpage}`);
      var param = {
        page: reqpage,
        size: this.size
      }
      counselApi.getCounselAll(param,
      (body)=>{
        if(body.data!=null && body.data.length>0){
          //this.list = body!=null? body : [];
          this.list = this.list.concat(body.data);
          this.curpage = reqpage;
        }
        this.isLoading=false;
      },
      (err)=>{
        console.log(err);
        this.isLoading=false;
      })
    },
    searchCounselByTag(hashtag){
      let URI = `/counsel/counselSearch?type=HASHTAG&keyword=${hashtag}`;
      this.$router.push(URI);
    },
    searchFirst(){
      var param = {
        page: 0,
        size: 1,
      }
      counselApi.getCounselAll(param,(body)=>{
        this.item = body!=null&&body.data.length>0? body.data[0] : [];
      })
    },
    getBackgroundUrl(idx){
      const size = this.backgroundUrls.length;
      const newidx = idx%size;
      return this.backgroundUrls[newidx];
    },
    detailCounsel(id){
      //alert(id);
      ///counsel/counselDetail
      const URI = `/counsel/counselDetail/${id}`;
      this.$router.push(URI);
    },
    doSearch(){
      const URI = `/common/search#tabs-2`;
      this.$router.push(URI);
    },
    handleScroll(e){
      if ((window.innerHeight + window.scrollY) >= document.body.scrollHeight && this.isLoading==false) {
        if(this.lastScrollY != window.scrollY){
          this.lastScrollY = window.scrollY;
          this.searchAllList();
        }else{
          this.lastScrollY = 0;
        }
      }
    }
  },
  created(){
    this.searchFirst();
    this.curpage=-1;
    this.list=[];
    this.searchAllList();
    window.addEventListener("scroll", this.handleScroll);
  },
  destroyed() {
    console.log('destroyed');
    window.removeEventListener("scroll", this.handleScroll);
  }
};
</script>

<style scoped>
.block{
    position:relative;
    background-size: cover;
}
.block:before{
  background-color:#33333388;
  content: '';
  display: block;
  height: 100%;
  position: absolute;
  width: 100%;
}
.counsel-txt{
  min-height:90px;
}

</style>