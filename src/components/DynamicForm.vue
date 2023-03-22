<template>
    <div class="container mt-4">
        <button @click="addProduct()" type="button" class="btn btn-primary">Add New</button>
        <div v-for="(product, index) in product" :key="index" class="row mt-3">
            <div class="col">
                <label for="">Product Name</label>
                <input v-model="product.productName" class="form-control form-control-lg" type="text" placeholder="" aria-label=".form-control-lg example">
            </div>
            <div class="col">
                <label for="">Product Price</label>
                <input v-model="product.productPrice" class="form-control form-control-lg" type="text" placeholder="" aria-label=".form-control-lg example">
            </div>

            <div class="col">
                <label for="">Qty</label>
                <input  @keyup="checkqty(index)" v-model="product.qty" class="form-control form-control-lg" type="number" placeholder="" aria-label=".form-control-lg example">
            </div>
            <div class="col">
                <label for="">Total</label>
                <input  v-model="product.total" class="form-control form-control-lg" type="text" placeholder="" aria-label=".form-control-lg example">
            </div>
            <div class="col">
                
                <button v-show="value1" @click="remove(index)" type="button" class="btn btn-danger mt-4">Remove</button>

            </div>
        </div>
        <div class="row mt-3">
            <div class="col">
                
            </div>
            <div class="col">
              
            </div>
         
            <div class="col">
            </div>
            <div class="col">
                <label for="">Grand Total</label>
                <input v-model="grandtotal" class="form-control form-control-lg" type="text" placeholder="" aria-label=".form-control-lg example">
            </div>
            <div class="col">
            </div>
        </div>
    

    </div>
</template>

<script>

  export default {
      name: 'DynamicForm',
      data() {
        return {
            product: [
                {
                    productName: "",
                    productPrice: "",
                    qty: "",
                    total:""
                   
                },
            ],
            grandtotal: ""
            
            
        };
      },
      methods: {
        addProduct() {
            this.product.push({
                productName:"",
                productPrice:"",
                qty: 1,
                total:""
            });
            this.value1 = true;

        },
        remove(index) {
            this.product.splice(index,1)
            console.warn(this.product.length)
            this.grandTotal(index);

            if(this.product.length <= 1){
                this.value1 = false;
            }


        },
        checkqty(index) {
            if(this.product[index].qty < 1){
                alert("qty cannot be less than 1");

            }else {
                this.sumTotal(index)
                this.grandTotal(index);
            }

        },
        sumTotal(index){
            this.product[index].total = this.product[index].qty * this.product[index].productPrice
        },
        sumGrandTotal(){

            return this.product.reduce((sum, product) => product.productPrice * product.qty + sum , 0)
 
        },

        grandTotal() {
           this.grandtotal = this.sumGrandTotal() 
           console.warn(this.grandtotal);
        },

      }
  }

</script>