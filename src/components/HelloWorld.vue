<template>
  <div class="vh-100 bg-white">
    <div class="row" style="margin: 0px 0px">
      <div class="col-md-3 col-sm-3 col-3">Detail</div>
      <div class="col-md-3 col-sm-3 col-3">
        <div>Name<span class="color-red">*</span></div>
        <div><select v-model="selected" class="form-control inputs" id="nama">
          <option value="0" selected>name</option>
          <option v-for="option in nama_employee" :key="option.id" v-bind:value="{value:option.value}">
            {{ option.text }}
          </option>
        </select></div>
      </div>
      <div class="col-md-3 col-sm-3 col-3"></div>
      <div class="col-md-3 col-sm-3 col-3"></div>
    </div>

    <div class="row m-t-20" style="margin-left: 0px;margin-right: 0px">
      <div class="col-md-3 col-sm-3 col-3"></div>
      <div class="col-md-3 col-sm-3 col-3">
        <div>Distribution Center<span class="color-red">*</span></div>
        <div><select class="form-control inputs" id="distribusi">
          <option value="" selected>DC Tanggerang</option>
          <option value="" >DC Cikarag</option>
        </select></div>
      </div>
      <div class="col-md-3 col-sm-3 col-3"></div>
    </div>

    <div class="row m-t-20" style="margin-left: 0px;margin-right: 0px">
      <div class="col-md-3 col-sm-3 col-3"></div>
      <div class="col-md-3 col-sm-3 col-3">
        <div>Payment Type<span class="color-red">*</span></div>
        <div><select class="form-control inputs" id="payment">
          <option value="" selected>1</option>
        </select></div>
      </div>
      <div class="col-md-3 col-sm-3 col-3">
        <div>Expired Day<span class="color-red">*</span></div>
        <div><select class="form-control inputs" id="ExpiredDate">
          <option value="" selected>1</option>
        </select></div>
      </div>
      <div class="col-md-3 col-sm-3 col-3"></div>
    </div>

    <div class="row m-t-20" style="margin-left: 0px;margin-right: 0px;border-bottom: 1px solid #EDEDED; padding-bottom: 20px">
      <div class="col-md-3 col-sm-3 col-3"></div>
      <div class="col-md-3 col-sm-3 col-3">
        <div>Note</div>
        <div><textarea style="width: 420px;height: 200px"></textarea></div>
      </div>
      <div class="col-md-3 col-sm-3 col-3">
        <div class="col-md-3 col-sm-3 col-3"></div>
      </div>
    </div>


    <div id="Product" style="padding: 20px 0px;">
      <div class="row m-t-20" style="margin-left: 0px;margin-right: 0px">
        <div class="col-md-3 col-sm-3 col-3">Product</div>
        <div class="col-md-3 col-sm-3 col-3">
          <div>Product<span class="color-red">*</span></div>
          <div><select class="form-control inputs" id="productselected">
            <option value="1" selected>orning Dew Milk</option>
            <option value="2" selected>Lee Mineral 600ml</option>
            <option value="3" selected>Greenfield Fuulcream Milk</option>
          </select></div>
        </div>
        <div class="col-md-3 col-sm-3 col-3">
          <div>unit<span class="color-red">*</span></div>
          <div><select class="form-control inputs">
            <option value="" v-for="listpack in barangBelanjaan" :key="listpack.id" selected>{{listpack.name}}</option>
          </select></div>
        </div>
        <div class="col-md-3 col-sm-3 col-3"></div>
      </div>

      <div class="row" style="margin: 0px 0px">
        <div class="col-md-3 col-sm-3 col-3"></div>
        <div class="col-md-3 col-sm-3 col-3">
          <div>Quantity<span class="color-red">*</span></div>
          <div><input type="tel" class="form-control" v-model="quality"  @keyup="hitungtotalprod" placeholder="0"></div>
        </div>
        <div class="col-md-3 col-sm-3 col-3">
          <div>Proce<span class="color-red">*</span></div>
          <div><input type="tel" class="form-control" v-model="nominal" @keyup="hitungtotalprod"   placeholder="0"></div>
        </div>
        <div class="col-md-3 col-sm-3 col-3">
          <div>Total Price <span class="color-red">*</span></div>
          <input type="tel" class="form-control" id=""  placeholder="0" v-model="nominalprod" disabled>
        </div>
      </div>
    </div>

    <div id="alltotal" class="m-t-20 m-b-20">
      <div class="row" style="margin: 0px 0px;border-bottom: 1px solid #EDEDED;">
        <div class="col-md-4 col-sm-4 col-4"></div>
        <div class="col-md-4 col-sm-4 col-4">
        </div>
        <div class="col-md-2 col-sm-2 col-2">
          <div class="font-weight-bold">Total</div>
        </div>
        <div class="col-md-2 col-sm-2 col-2">
          <div class="font-weight-bold" >{{this.nominalprod}}</div>
        </div>
      </div>
    </div>

    <div id="button">
      <div class="row" style="margin: 0px 0px;border-bottom: 1px solid #EDEDED;">
        <div class="col-md-5 col-sm-5 col-5"></div>
        <div class="col-md-5 col-sm-5 col-5">
        </div>
        <div class="col-md-1 col-sm-1 col-1">
          <div class="font-weight-bold" @click="select">Cancel</div>
        </div>
        <div class="col-md-1 col-sm-1 col-1">
          <button type="button" class="btn btn-success" disabled @click="select">Confirm</button>
        </div>
      </div>
    </div>

<!--    <div class="row m-t-20" style="margin-left: 0px;margin-right: 0px">-->
<!--      <div class="col-md-3 col-sm-3 col-3">Product</div>-->
<!--      <div class="col-md-3 col-sm-3 col-3">-->
<!--        <div>Product<span class="color-red">*</span></div>-->
<!--        <div><select class="form-control inputs" id="productselected">-->
<!--          <option value="" selected>1</option>-->
<!--        </select></div>-->
<!--      </div>-->
<!--      <div class="col-md-3 col-sm-3 col-3">-->
<!--        <div>unit<span class="color-red">*</span></div>-->
<!--        <div><select class="form-control inputs" id="productselected">-->
<!--          <option value="" selected>1</option>-->
<!--        </select></div>-->
<!--      </div>-->
<!--      <div class="col-md-3 col-sm-3 col-3"></div>-->
<!--    </div>-->


  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data(){
    return{
      nama_employee:[],
      selected:'',
      quality:0,
      nominal:0,
      nominalprod:0,
      barangBelanjaan: [
        { name: 'pak', price: 10000, id:1},
        { name: 'pcs', price: 1000, id:2},
        { name: 'karton', price: 100, id:3 }
      ]

    }
  },
  mounted() {
    this.getdataselect();
  },
  methods:{
    async getdataselect(){
      try {
        const res = await this.$axios.get(this.$baseurl + '/api/v1/employees');
        if(res.status===200) {
          var employee = res.data.data;
          for (var i = 0; i < employee.length; i++) {
            this.nama_employee.push({
              value: employee[i].id,
              text: employee[i].employee_name
            })
          }
        }
      }catch (e) {
        alert('error')
      }
    },

    select(){
      console.log(this.selected)
    },

    hitungtotalprod(){
      this.nominalprod = this.quality * this.nominal

    },

    // checkvalidate(){
    //   var select = this.selected;
    //   if (select !== '') {
    //     $('#btnNext').prop('disabled', false);
    //     $('#anotherButton').prop('disabled', false)
    //   } else {
    //     $('#btnNext').prop('disabled', true);
    //     $('#anotherButton').prop('disabled', true)
    //   }
    // }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
