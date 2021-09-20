<template>

<div class="flex justify-center p-4" >

<div  >

    <div class="payments flex flex-wrap w-full my-2">

        <div class="monthlypayments lg:w-1/2 p-2 ">
            <div class="title">Max Loan Amount</div>
            <div class="amount"><moneyformat :amount="loanAmount"/></div>
        </div>

        <div class="monthlypayments lg:w-1/2 p-2 ">
            <div class="title">Monthly payment</div>
            <div class="amount"><moneyformat :amount="monthlyPayment"/></div>
        </div>


        <div class="monthlypayments lg:w-1/2 p-2">
            <div class="title">Total Interest</div>
            <div class="amount"> <moneyformat :amount="interest"/></div>
        </div>


        <div class="monthlypayments lg:w-1/2 p-2">
            <div class="title">Total payment</div>
            <div class="amount"> <moneyformat :amount="totalPayment"/> </div>
        </div>


        

    </div>



  <div class="calculator py-4">
      <div class="title text-center">
          Loan Calculator
      </div>


      <div class="form py-4">

          <div class="inputsection">
              <div class="inputtitle">
                 Your shares
              </div>
              <input type="text" name="" id="" v-model.number="amount">
          </div>


          <div class="inputsection">
              <div class="inputtitle">
                 Loan Plan
              </div>


              <select name="loantype" id="loantype" v-model="plan">
                  <option :value="option" v-for="option in plans" :key="option.max+option.name +option.rate" class="flex">

                    <div class="flex justify-between w-full">
                        <div class="pr-6">{{option.name}}</div>

                        <div>({{option.rate}}%)</div>
                        
                    </div>  
                    </option>
              </select>
              
              
          </div>


          <div class="inputsection">
              <div class="inputtitle">
                Interest Rate (%)
              </div>
              <input type="number" name="" id="" v-model="plan.rate">
          </div>


          <div class="inputsection">
              <div class="inputtitle">
                Months to repay
              </div>
              <input type="number" name="" id="" v-model="plan.period">
          </div>




      </div>


  </div>
</div>

</div>
</template>

<script>
export default {

    data() {
        return {

            amount:null,

            plan:{
                name:"Asset Financing",
                rate:14,
                period:40,
                max:99999999,
            },

            duration:12,

            paymentPlans:[
                {
                    name:"plan 1",
                    rate:5,
                },
                {
                    name:"plan 2",
                    rate:8,
                },
                {
                    name:"plan 3",
                    rate:12,
                },
                {
                    name:"plan 4",
                    rate:14,
                }
            ]
        }
    },

    computed:{
        plans(){
            return this.$store.state.plans
        },
        loanAmount(){

            if(!this.amount){
                return 0
            }
           return this.amount*3
        },
        interest(){
            let rate=this.plan.rate / 100
            if(!this.loanAmount){
                return 0
            }

            return (this.loanAmount *rate);
        },

        totalPayment(){
            let total=this.loanAmount+this.interest;
            return  parseInt(total);

        },

        monthlyPayment(){
            let monthlypay=this.totalPayment/this.plan.period;
            return parseInt(monthlypay);

        }
    }

}
</script>

<style>
.payments .monthlypayments{
   padding: 1rem;
}

.payments{
    padding: 1rem;
    /* border:1px solid #242265 ;
    border:1px solid #24226577 ; */
    border-radius: 12px;
    background: #f3f4f8;
    border-radius: 8px;

}

.payments .title{
    font-weight: bold;
    font-size: 14px;
}

.payments .amount{
    white-space: nowrap;
    /* font-size: 26px;
    font-weight: bold; */
}
.calculator .title{
    font-family: Poppins, sans-serif;
    color: #242265;
    font-size: 24px;
    line-height: 36px;
    font-weight: 700;
    margin-bottom: 12px;
}

.payments .title{
    white-space: nowrap;
}

.calculator .form{
    max-width: 600px;
    width: 100%;
}

.calculator .inputtitle{
    font-weight: 600;
    font-size: 14px;
    margin: 2px 0px;
}

.calculator .form input,.calculator .form select{
    display: block;
    width: 100%;
    height: 38px;
    padding: 8px 12px;
    margin-bottom: 10px;
    font-size: 14px;
    line-height: 1.42857143;
    color: #333333;
    background-color: #ffffff;
    border: 1px solid #cccccc;
    border-radius: 6px;
}

</style>