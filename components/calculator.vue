<template>

<div class="calculatorwrap flex justify-center p-4" >

<div class="w-full">

    <div class="largescreen" >

        <h4>
            Your results
        </h4>

    </div>

    <div class="payments largescreen flex flex-wrap w-full my-2">

        <div class="column-1">

            <div class="w-full ">

                <div class="monthlypayments payment borderbottomlight  w-full  flex items-center justify-between ">
                    <div class="title  flex items-center">
                    <moneybagicon/>  Max Loan Amount
                    </div>
                    <div class="amount"><moneyformat :amount="loanAmount"/></div>
                </div>

            </div>


            <div class="w-full ">

                <div class="monthlypayments payment w-full  flex items-center justify-between ">
                    <div class="title flex items-center">
                    <rateicon/>  Total Interest
                    </div>
                    <div class="amount"> <moneyformat :amount="interest"/></div>
                </div>

            </div>



        </div>


        <div class="column-2">

            
            <div class=" w-full ">

                <div class="monthlypayments payment borderbottomlight  flex items-center justify-between ">

                    <div class="title  flex items-center">
                    <calendericon/>  Monthly payment
                    </div>
                    <div class="amount"><moneyformat :amount="monthlyPayment"/></div>

                </div>

            </div>


            <div class="monthlypayments payment w-full  flex items-center justify-between">

                    <div class="title flex items-center">
                    <moneyicon/> Total payment
                    </div>
                    <div class="amount"> <moneyformat :amount="totalPayment"/> </div>

            </div>

            
        </div>

        


       


        

    </div>



  <div class="calculator py-4">
     


      <div class="form py-4 flex flex-wrap">


        <div class="column-1">

            <div class="inputsection w-full">

              <div class="inputtitle">
                 Your shares
              </div>
              <input placeholder="Your total shares in nacico" type="text" name="" id="" v-model.number="amount" min="0" :max="plan.max">
         
            </div>  

          <div class="inputsection w-full ">
              <div class="inputtitle">
                Interest Rate (%)
              </div>
              <input type="number" name="" id="" v-model="plan.rate" disabled>
          </div>


        </div>


        <div class="column-2">

          <div class="inputsection w-full ">

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


          <div class="inputsection w-full">
              <div class="inputtitle">
                Months to repay
              </div>
              <input type="number" name="" id="" v-model="plan.period" disabled>
          </div>

          </div>


      </div>

    <div class="smallscreen" >

        <h4>
            Your results
        </h4>

    </div>


    
    <div class="payments smallscreen flex flex-wrap w-full my-2">

        <div class="w-full md:w-1/2 lg:w-1/2 lg:pr-6">

            <div class="monthlypayments payment borderbottomlight  w-full    ">
                <div class="title  flex items-center">
                <moneybagicon/>  Max Loan Amount
                </div>
                <div class="amount px-10"><moneyformat :amount="loanAmount"/></div>
            </div>

        </div>

        <div class=" w-full md:w-1/2 lg:w-1/2 ">

            <div class="monthlypayments payment borderbottomlight   ">

                <div class="title  flex items-center">
                <calendericon/>  Monthly payment
                </div>
                <div class="amount px-10"><moneyformat :amount="monthlyPayment"/></div>

            </div>

        </div>

        
        <div class="w-full md:w-1/2 lg:w-1/2 lg:pr-6">

        <div class="monthlypayments payment w-full  ">
            <div class="title flex items-center">
              <rateicon/>  Total Interest
            </div>
            <div class="amount px-10"> <moneyformat :amount="interest"/></div>
        </div>

         </div>




        <div class="monthlypayments payment w-full md:w-1/2 lg:w-1/2 ">

                <div class="title flex items-center">
                <moneyicon/> Total payment
                </div>
                <div class="amount px-10"> <moneyformat :amount="totalPayment"/> </div>

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

.calculatorwrap{
    
    overflow: hidden;
    width: 100%;
    left: 250px;
    top: 409px;
    border-radius: 8px;
    border: 1px solid #F1F3F5;
    padding: 2rem 2.6rem;
    box-shadow: 0px 4px 14px 1px #2B374121;


}

.calculatorwrap svg{
    width: 24px;
    margin-right:12px ;
}

.calculatorwrap h4{

    font-size: 24px;
    font-style: normal;
    font-weight: 500;
    line-height: 36px;
    letter-spacing: 0em;
    text-align: left;
    color: #202930;

}


.payments .monthlypayments{
   padding-top:1.6rem ;
   padding-bottom:1.6rem;
}



.payments{

    padding: .6rem 0px;
    overflow: hidden;
    border-bottom: 3px solid #A8A7C1;
    color: #202930;
    padding-bottom: 1.6rem;
    margin-bottom: 1rem;

}

.payments .amount{
    font-weight: 500;
    font-size: 16px;
    line-height: 22px;
}

.payments .title{
    white-space: nowrap;
    font-weight: 500;
    font-size: 16px;
    line-height: 22px;
}

.payments .amount{

    white-space: nowrap;

}

.calculatorwrap .borderbottomlight{

    border-bottom: 1px solid #E5E9EC;

}

.calculator .title{

    font-family: Poppins, sans-serif;
    color: #242265;
    font-size: 24px;
    line-height: 36px;
    font-weight: 700;
    margin-bottom: 12px;

}



.calculator .form{
    width: 100%;
}

.calculatorwrap .column-1,.calculatorwrap .column-2{
    width: 50%;
    
}

.calculatorwrap .column-1{
  
    padding-right: 1rem;
}

.calculator .inputtitle{
   
    font-size: 16px;
    font-style: normal;
    font-weight: 400;
    line-height: 32px;
    letter-spacing: 0em;
    text-align: left;
    color: #405261;

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


    height: 64px;
    width: 100%;
    top: 800px;
    border-radius: 4px;

}

.smallscreen{
    display: none;
}

@media (max-width:600px) {

.calculatorwrap{
    padding: .8rem;
}

.largescreen{
    display: none;
}

.smallscreen{
    display: flex;
}


.calculatorwrap .column-1,.calculatorwrap .column-2{
    width: 100%;
    
}

.calculatorwrap .column-1{
  
    padding-right: 0rem;
}

}



</style>