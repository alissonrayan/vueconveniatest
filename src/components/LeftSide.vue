<template>
    <div class="left-content">
        <p class="left-content__text">
            Olá,<br /><br />
            Você está acessando o <span>Convenia</span><br />
            que oferece descontos e vantagens<br />
            em mais de 5.000 estabelecimentos.<br />
            Economize na compra de produtos<br />
            e serviços de marcas que interessam.
        </p>
        <div class="left-content__fields">
            <div class="left-content__fields__cpf">
                <input type="text" v-model="cpf" required placeholder="ativar CPF">
                <button v-on:click="cpfvalid()">Ok</button>
            </div>
            <div class="left-content__fields__login">
                <p class="left-content__fields__login__text">Se você já possuir cadastro, <span>faça login</span></p>
                <br />
                <input type="email" v-model="mail" required placeholder="e-mail">
                <input type="password" v-model="pass" required placeholder="senha" pattern=".{6,}" title="É necessário ter 6 caracteres ou mais!">
                <button v-on:click="add()">Entrar</button>
                <br />
                <a href="https://www.convenia.com.br/lembrar">Esqueci a senha</a>
            </div>
        </div>
    </div>
</template>
<script>

import axios from 'axios';

export default {
  name: 'LeftSide',
  data (){
      return{
          mail: '',
          pass: '',
          cpf: ''
      }
  },
  methods: {
      add(){
        if(this.mail != '' && this.pass != ''){
            axios.post('https://convenia-front-end-test.firebaseio.com/users.json', {
                email: this.mail,
                password: this.pass
            })
            .then(function (response) {
                console.log(response);
            })
            .catch(function (error) {
                console.log(error);
            });
            this.mail = ''
            this.pass = ''
        }
        else{
            alert("Campos vazios, por favor informe os dados!")
        }
      },
    cpfvalid(){
        if(this.cpf.length !=11 || this.cpf == "00000000000" || this.cpf == "11111111111" || this.cpf == "22222222222" ||
            this.cpf == "33333333333" || this.cpf == "44444444444" || this.cpf == "55555555555" ||
            this.cpf == "66666666666" || this.cpf == "77777777777" || this.cpf == "88888888888" ||
            this.cpf == "99999999999"){
                this.cpferro();
        }
        else{
            let cpfnumber = this.cpf;
            let cpfarr = cpfnumber.toString(11).split('');
            let aux = 10;
            let soma = 0;
            
            for(var i = 0; i <= 8; i++){
            soma = soma + cpfarr[i]*aux;
            aux = aux -1;
            }
            aux = 11-(soma%11);
            if(aux> 9){
                if(cpfarr[9] != 0){
                    alert("CPF INVALÍDO! Por favor, informe um CPF correto");
                    return 0;
                }
            }else{
                if(cpfarr[9] != aux){
                    alert("CPF INVALÍDO! Por favor, informe um CPF correto");
                    return 0;
                }
            }
            aux = 11;
            soma = 0;

            for(var i = 0; i <= 9; i++){
                soma = soma + cpfarr[i]*aux;
                aux = aux -1;
            }
            aux = 11-(soma%11);
            if(aux> 9){
                if(cpfarr[10] != 0){
                    alert("CPF INVALÍDO! Por favor, informe um CPF correto");
                    return 0;
                }
            }else{
                if(cpfarr[10] != aux){
                    alert("CPF INVALÍDO! Por favor, informe um CPF correto");
                    return 0;
                }
            }

            alert("CPF VALÍDO! Direcionando para a página...")
        }
    },
    cpferro(){
        alert("CPF INVALÍDO! Por favor, informe um CPF correto");
        this.limparcampo();
        return 0;
    },
    limparcampo(){
        this.cpf = ''
    }

  }
}
</script>
<style lang="scss">

    @import '../assets/css/util.scss';

    .left-content{
        padding: 20px 0px 20px 20px;

        @include sm{
            padding: 60px 0 0 0;
        }
        @include md{
            padding: 80px 0 0 0;
        }
        &__text{
            font-size: 14px;
            padding-bottom: 50px;

            @include sm{
                font-size: 16px;
                padding-left: 40px;
            }
            @include md{
                font-size: 20px;
            }

            span{
                color: #b43ef6;
            }
        }

        &__fields{
            padding-left: 0;
            @include sm{
                padding-left: 40px;
            }

            &__cpf{
                margin: 30px 0;

                @include inp;

                @include btn;
            }

            &__login{
                @include inp;
                @include btn;

                &__text{
                    margin: 5px 0px;
                    font-size: 14px;
                }
                button{
                    border-radius: 12px;
                    padding: 4px 20px;
                }
                input{
                    margin: 5px 0;
                }
                span{
                    color: #b43ef6;
                }
                a{
                    text-decoration: none;
                    color: #b43ef6;
                }
            }
        }
    }
</style>
