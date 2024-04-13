<template>
  <h1>CRYPTO</h1>
  <Input :changeAmount="changeAmount" :convert="convert" />
  <p v-if="error != ''">{{ error }}</p>
  <p v-if="result != 0" className="result-text">{{ result }}</p>
  <div className="selectors">
  <Selector :setCrypto="setCryptoFirst" />  
   <Selector :setCrypto="setCryptoSecond" /> 
   
</div>

</template>

<script>
import Input from './components/Input.vue'
import Selector from './components/Selector.vue'
import CryptoConvert from 'crypto-convert';

const convert = new CryptoConvert();

export default{
  components: { Input, Selector },
  data(){
    return{
      amount:0,
      cryptoFirst: '',  //создаем переменные для первого и второго столбца
      cryptoSecond: '',
      error: '',
      result: 0
    }
      },
methods:{
  changeAmount(val){
    this.amount = val  //передаем значение input, которое ввел пользователь
  },
  setCryptoFirst(val){
    this.cryptoFirst = val  //передаем значение первого столбца, выбрал пользователь
  },
  setCryptoSecond(val){
    this.cryptoSecond = val //передаем значение второго столбца, выбрал пользователь
  },
 async convert(){ //обязательно прописываем async, так как иначе await выдаст ошибку
if (this.amount <=0){
  this.error = "Enter a number greater than 0"; //проверяем на наличие ошибок
  return;
} else if (this.cryptoFirst == '' || this.cryptoSecond == ''){
  this.error = "Сhoose a currency";
  return;
} else if (this.cryptoFirst == this.cryptoSecond){
  this.error = "Сhoose a different currency";
  return;
}
this.error = ''; // если ошибок больше нет, очищаем предыдущие ошибки
  await convert.ready(); 
  this.result = convert.BTC.USD(this.amount)
  
  if (this.cryptoFirst == 'BTC' && this.cryptoSecond == 'ETH')
  this.result = convert.BTC.ETH(this.amount);
  else if (this.cryptoFirst == 'BTC' && this.cryptoSecond == 'USDT')
  this.result = convert.BTC.USDT(this.amount);
  else if (this.cryptoFirst == 'ETH' && this.cryptoSecond == 'BTC')
  this.result = convert.ETH.BTC(this.amount);
  else if (this.cryptoFirst == 'ETH' && this.cryptoSecond == 'USDT')
  this.result = convert.ETH.USDT(this.amount);
  else if (this.cryptoFirst == 'USDT' && this.cryptoSecond == 'BTC')
  this.result = convert.USDT.BTC(this.amount);
  else if (this.cryptoFirst == 'USDT' && this.cryptoSecond == 'ETH')
  this.result = convert.USDT.ETH(this.amount);
  

  }
  }
}
  


</script>

<style scoped>
 .result-text{
  font-family: 'Nabla', cursive ;
  font-size: 2em;
 }
 .selectors{
  display: flex;
  justify-content: space-around;
  width: 700px;
  margin: 0 auto;
 }
</style>
