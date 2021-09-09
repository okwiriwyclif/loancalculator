<template class="border-0">


    <span class="numberformat inline-block m-0 p-0 border-0 ">
     {{currency}} {{formatedNumber}}
    </span>


  
</template>

<script>
export default {
props:['amount'],
computed:{
    formatedNumber(){
        let number =this.amount;
        if(!this.amount){
            number=0;
        }
        let newNumber=Number(Math.round(number + 'e2') + 'e-2').toFixed(2);
        let finalNumber= new Intl.NumberFormat('en-US', {
                minimumFractionDigits: 2,      
                maximumFractionDigits: 2,
                }).format(newNumber);
        return finalNumber ;
    },
    currency(){
        return 'Ksh'
    }
}
}
</script>

<style>
</style>