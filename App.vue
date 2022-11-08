<template>
    <div :class="classBinding">
        <input v-model="inputString"/>
        <template v-for="button in buttons">
            <button v-if="isClearButton(button.innerText)" @click="Clear()">{{button.innerText}}</button>
            <button v-else-if="isCalculateButton(button.innerText)" @click="Calculate()">{{button.innerText}}</button>
            <button v-else @click="Append(button.innerText)">{{button.innerText}}</button>
        </template>
    </div>
</template>

<script>
    export default{
        data(){
            return{
                inputString: '',
                classBinding: 'content',
                buttons:[{innerText:'1'}, {innerText:'2'}, {innerText:'3'}, {innerText:'+'},
                {innerText:'4'}, {innerText:'5'}, {innerText:'6'}, {innerText:'-'},
                {innerText:'7'}, {innerText:'8'}, {innerText:'9'}, {innerText:'*'},
                {innerText:'='}, {innerText:'C'}, {innerText:'.'}, {innerText:'/'},],
                actions:'+-*/.'
            }   
        },
        methods:{
            Clear(){    
                this.inputString = '';
            },
            Append(str){
                this.inputString += str;
            },
            isValid(str){
                for(var char of str){
                    if(isNaN(char) && !this.actions.includes(char)){
                        alert("There is error in the input field!")
                        return false
                    }
                }

                if(this.actions.includes(str[str.length - 1]) || (this.actions.includes(str[0]) && str[0] != '-' &&  str[0] != '+')){
                    alert("There is error in the input field!")
                    return false
                }
                
                for(let i = 0; i < str.length - 1; i++){
                    if(str[i] == str[i + 1] && this.actions.includes(str[i])){
                        alert("There is error in the input field!")
                        return false
                    }
                }
                return true
            },
            Calculate(){
                if(this.isValid(this.inputString)){
                    this.inputString = eval(this.inputString)
                }
            },
            isClearButton(str){
                if(str == 'C') return true
                else return false
            },
            isCalculateButton(str){
                if(str == '=') return true
                else return false
            }
        }
    }
</script>

<style>
button{
    border-radius: 15%;
    margin: 5px;
    height: 70px;
    width: 70px;
}
input{
    font-size: larger;
    border-radius: 15px;
    margin: 5px;
    width: 90%;
    height: 50px;
}
.content{
    width: 350px;
    border: solid black 3px;
    border-radius: 15px;
    display: inline-flexbox;
    background-color: rgb(198, 198, 198);
    text-align: center;
}
</style>