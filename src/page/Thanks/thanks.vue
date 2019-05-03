<template>
  <div>
  

    <div id="SOHUCS" sid="123456" style="width:1218px;"></div>
  </div>
</template>
<script>
  import { thank, thanksList } from '/api/index.js'
  import YShelf from '/components/shelf'
  import product from '/components/product'
  import mallGoods from '/components/mallGoods'
  require('../../../static/changyan/changyan.js')
  export default {
    data () {
      return {
        thankPanel: [],
        tableData: [],
        currentPage: 1,
        pageSize: 10,
        total: 0,
        loading: true
      }
    },
    methods: {
      handleSizeChange (val) {
        this.pageSize = val
        this._thanksList()
        this.loading = true
      },
      handleCurrentChange (val) {
        this.currentPage = val
        this._thanksList()
        this.loading = true
      },
      _thanksList () {
        let params = {
          params: {
            size: this.pageSize,
            page: this.currentPage
          }
        }
        thanksList(params).then(res => {
          this.loading = false
          this.tableData = res.result.data
          this.total = res.result.recordsTotal
        })
      }
    },
    mounted () {
      thank().then(res => {
        let data = res.result
        this.thankPanel = data[0]
      })
      this._thanksList()
      window.changyan.api.config({
        appid: 'cyrV7vlR4',
        conf: 'prod_3163726f95fdac5ad0531c2344fc86ea'
      })
    },
    components: {
      YShelf,
      product,
      mallGoods
    }
  }
</script>
<style lang="scss" rel="stylesheet/scss" scoped>
  .sk_item {
    width: 170px;
    height: 225px;
    padding: 0 14px 0 15px;
    > div {
      width: 100%;
    }
    a {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      transition: all .3s;
      &:hover {
        transform: translateY(-5px);
      }
    }
    img {
      width: 130px;
      height: 130px;
      margin: 17px 0;
    }
    .sk_item_name {
      color: #999;
      display: block;
      max-width: 100%;
      _width: 100%;
      overflow: hidden;
      font-size: 12px;
      text-align: left;
      height: 32px;
      line-height: 16px;
      word-wrap: break-word;
      word-break: break-all;
    }
    .sk_item_price {
      padding: 3px 0;
      height: 25px;
    }
    .price_new {
      font-size: 18px;
      font-weight: 700;
      margin-right: 8px;
      color: #f10214;
    }
    .price_origin {
      color: #999;
      font-size: 12px;
    }
  }

  .box {
    overflow: hidden;
    position: relative;
    z-index: 0;
    margin-top: 29px;
    box-sizing: border-box;
    border: 1px solid rgba(0, 0, 0, .14);
    border-radius: 8px;
    background: #fff;
    box-shadow: 0 3px 8px -6px rgba(0, 0, 0, .1);

  }

  ul.box {
    display: flex;
    li {
      flex: 1;
      img {
        display: block;
        width: 305px;
        height: 200px;
      }
    }
  }

  .mt30 {
    margin-top: 30px;
  }

  .hot {
    display: flex;
    > div {
      flex: 1;
      width: 25%;
    }
  }

  .table {
    align-items: center;
    display: flex;
    flex-direction: column;
    p{
      font-size: 18px;
      margin-top: 2vw;
      // color: #5683EA;
    }
    .el-table{
      // margin: 5vw 8vw 2vw 8vw;
      margin: 2vw 0 2vw 0vw;
    }
    .el-pagination{
      align-self: flex-end;
      margin: 0 3.5vw 2vw;
    }
  }

  .donate {
    // align-items: center;
    display: flex;
    flex-direction: column;
    margin: 1vw 3vw 2vw 3vw;
    p{
      font-size: 16px;
      margin-top: 1vw;
    }
  }

  .floors {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    .imgbanner {
      width: 50%;
      height: 430px;
    }
    img {
      display: block;
      width: 100%;
      height: 100%;
    }
  }

</style>
