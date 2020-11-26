<template>
  <div>
    <form>
      <input
        type="text"
        value=""
        v-model="upload.type"
        placeholder="请输入上传类型"
      />
      <input type="file" @change="getFile($event)" />
      <button @click="submitForm($event)">提交</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      warehouse: {
        startDate: "",
        endDate:""
      },
      upload:{
           type: ""
      },
      TotalStockOut:{}
    };
  },
  

// mounted:function(){
//       this.showData();//需要触发的函数
// },
  methods: {
      showss(){
          alert(111);
      },
    getFile(event) {
      this.file = event.target.files[0];
      console.log(this.file);
    },
    // test(){
    //     let config = {
    //     headers: {
    //       "Content-Type": "application/json",
    //       "Authorization":"eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJyb290IiwicGFzc3dvcmQiOiJyb290IiwiZXhwIjoxNjA2MzY2Mjg5LCJpYXQiOjE2MDYzNjI2ODksImp0aSI6ImVkNDQ3ZTEyLTJkNTMtNGM2NC04YjFjLThhNGQ5NjEwMWYyNCIsInVzZXJuYW1lIjoicm9vdCJ9.DUhupfEStFbE9l4bSAXB-NIeCQbDhyGyyyNBHBMIy24"
    //     },
    //   };

    //   this.$axios({
    //     method: "post",
    //     url: "http://192.168.10.7:8081/sales/getSalesWarehouseOutData",
    //     data: {"startDate":"123",
    //             "endDate":"456"},
    //     headers: {
    //         "Content-Type": "application/json",
    //       "Authorization":"eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJyb290IiwicGFzc3dvcmQiOiJyb290IiwiZXhwIjoxNjA2MzY2Mjg5LCJpYXQiOjE2MDYzNjI2ODksImp0aSI6ImVkNDQ3ZTEyLTJkNTMtNGM2NC04YjFjLThhNGQ5NjEwMWYyNCIsInVzZXJuYW1lIjoicm9vdCJ9.DUhupfEStFbE9l4bSAXB-NIeCQbDhyGyyyNBHBMIy24"
        
    //     }
                
    //   })
    //     .then((response) => {
    //       alert("上传完成");
    //     })
    //     .catch((err) => {
    //       alert(err);
    //     });
    // },
showData(){
    let that=this;
let config = {
          "Content-Type": "multipart/form-data"
        //   "Authorization":"eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJyb290IiwicGFzc3dvcmQiOiJyb290IiwiZXhwIjoxNjA2MzY2Mjg5LCJpYXQiOjE2MDYzNjI2ODksImp0aSI6ImVkNDQ3ZTEyLTJkNTMtNGM2NC04YjFjLThhNGQ5NjEwMWYyNCIsInVzZXJuYW1lIjoicm9vdCJ9.DUhupfEStFbE9l4bSAXB-NIeCQbDhyGyyyNBHBMIy24"
      };
this.$axios({
        method: "post",
        url: "http://192.168.10.7:8081/sales/getSalesWarehouseOutData",
        data: this.warehouse,
        headers: config,
      })
        .then((response) => {
            that.TotalStockOut=response.data;
          alert(response);
        })
        .catch((err) => {
          alert(err);
        });
    },

    submitForm(event) {
        debugger
      event.preventDefault();
      let formData = new FormData();
      debugger
      formData.append("type", this.upload.type);
      formData.append("file", this.file);
      let config = {
          "Content-Type": "multipart/form-data",
          "Authorization":"eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJyb290IiwicGFzc3dvcmQiOiJyb290IiwiZXhwIjoxNjA2MzY2Mjg5LCJpYXQiOjE2MDYzNjI2ODksImp0aSI6ImVkNDQ3ZTEyLTJkNTMtNGM2NC04YjFjLThhNGQ5NjEwMWYyNCIsInVzZXJuYW1lIjoicm9vdCJ9.DUhupfEStFbE9l4bSAXB-NIeCQbDhyGyyyNBHBMIy24"
      };

      this.$axios({
        method: "post",
        url: "http://192.168.10.7:8081/sales/getExcleWarehousing",
        data: formData,
        headers: config,
      })
        .then((response) => {
          alert("上传完成");
        })
        .catch((err) => {
          alert(err);
        });
    },
    
},

    
};
</script>
