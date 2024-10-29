<template>
   <v-container>
      <v-row align="center" justify="center">
         <v-col cols="12" sm="10">
            <v-card class="elevation-6 mt-10">
               <v-window v-model="step">
                  <!-- LOGIN -->
                  <v-window-item :value="1">
                     <v-row>
                        <v-col cols="12" lg="6">
                           <v-card-text class="mt-12">
                              <h4 class="text-center text-h5">Faça login com suas credenciais</h4>
                              <h6 class="text-center grey--text text-subtitle-2">Entre na sua conta para continuar
                                 gerenciando <br>e editando o fluxo da sua clínica
                              </h6>
                              <v-row class="mt-10" align="center" justify="center">
                                 <v-col cols="12" sm="8">
                                    <!-- EMAIL INPUT -->
                                    <v-text-field label="Email" outlined dense color="primary_green_color" autocomplete="false"
                                       append-inner-icon="mdi-email" v-model="login.email" />
                                    <!-- PASSWORD INPUT -->
                                    <v-text-field class="password-field" label="Senha" dense color="primary_green_color"
                                       autocomplete="false" clearable v-model="login.password"
                                       :type="utils.showPassword ? 'text' : 'password'">
                                       <template v-slot:append-inner>
                                          <v-icon @click="toggleShowPassword">
                                             {{ utils.showPassword ? 'mdi-eye' : 'mdi-eye-off' }}
                                          </v-icon>
                                       </template>
                                    </v-text-field>

                                    <div class="d-flex justify-space-between align-center">
                                       <v-checkbox label="Lembrar-me" color="primary_green_color" v-model="login.remember" />
                                       <span class="caption primary_green_color mt-n5 cursor-pointer"
                                          @click.stop.prevent="utils.forgotPassword = true">Esqueceu sua
                                          senha ?</span>
                                    </div>
                                    <v-dialog v-model="utils.forgotPassword" max-width="400" persistent>
                                       <v-card>
                                          <v-card-title class="text-h5">
                                             Recuperação de senha
                                          </v-card-title>
                                          <v-divider></v-divider>
                                          <v-card-text>
                                             <v-text-field density="compact" label="Email" outlined dense color="primary_green_color"
                                                autocomplete="false" append-inner-icon="mdi-email-outline"
                                                :rules="rule.email" v-model="recoveryLogin"></v-text-field>
                                             <v-spacer></v-spacer>
                                             <v-card variant="tonal mt-2">
                                                <v-card-text class="text-caption">
                                                   <strong class="text-warning">Recuperação de senha:</strong>
                                                   Por favor, insira o seu email já cadastrado em nosso sistema, você
                                                   receberá um email com um link para redefinir sua senha.
                                                </v-card-text>
                                             </v-card>
                                          </v-card-text>
                                          <v-divider></v-divider>
                                          <v-card-actions>
                                             <v-btn class="bg-red" @click="utils.forgotPassword = false">Fechar</v-btn>
                                             <v-spacer></v-spacer>
                                             <v-btn :loading="utils.loader" class="bg-blue"
                                                @click="sendEmailToRecoveryPassword">
                                                Enviar
                                             </v-btn>
                                          </v-card-actions>
                                       </v-card>
                                    </v-dialog>

                                    <v-btn class="mb-10" color="primary_green_color" rounded="1" dark block tile>Entrar</v-btn>

                                 
                                    
                                    <div class="d-flex justify-space-around align-center mx-16 mb-16">
                                       <v-btn depressed outlined variant="tonal" class="rounded-circle icons__rounded">
                                          <v-icon color="blue">mdi-facebook</v-icon>
                                       </v-btn>
                                       <v-btn depressed outlined variant="tonal" class="rounded-circle icons__rounded">
                                          <v-icon color="red">mdi-google</v-icon>
                                       </v-btn>
                                       <v-btn depressed outlined variant="tonal" class="rounded-circle icons__rounded">
                                          <v-icon color="light-blue lighten-3">mdi-twitter</v-icon>
                                       </v-btn>
                                    </div>
                                   
                                 </v-col>
                              </v-row>
                           </v-card-text>
                        </v-col>
                        <v-img cover aspect-ratio="16/9" cols="12" lg="6"
                           src="https://versatilis.com.br/wp-content/uploads/2023/04/recepcionista-de-clinica-consultorio.jpg">

                           <v-col class="card__info">
                              <v-card class="pa-5 card__login">
                                 <v-card-text class="white--text text-center">
                                    <h3 class="text-h5">Ainda não tem uma conta ?</h3>
                                    <h6 class="text-subtitle-2">
                                       Vamos preparar tudo para que você possa começar a criar sua primeira
                                       <br> experiência com o <span class="caption primary_green_color" >ProntuárioX</span>
                                    </h6>
                                 </v-card-text>
                                 <div class="text-center">
                                    <v-btn tile outlined dark @click="step++">Registre-se</v-btn>
                                 </div>
                              </v-card>
                           </v-col>

                        </v-img>

                     </v-row>
                  </v-window-item>
                  <!-- REGISTER -->
                  <v-window-item :value="2">
                     <v-row>
                        <v-img cover aspect-ratio="16/9" cols="12" lg="6"
                           src="https://www.linimarstoque.com.br/wp-content/uploads/2024/07/CLINICA-MEDICA-4.jpg">

                           <v-col class="card__info">
                              <v-card class="pa-5 card__register">
                                 <v-card-text class="white--text text-center">
                                    <h3 class="text-h5">Já é inscrito ?</h3>
                                    <h6 class="text-subtitle-2">
                                       Entre na sua conta para continuar gerenciando <br>e editando o fluxo da sua
                                       clínica
                                    </h6>
                                 </v-card-text>
                                 <div class="text-center">
                                    <v-btn tile outlined dark @click="step--">Registre-se</v-btn>
                                 </div>
                              </v-card>
                           </v-col>
                        </v-img>

                        <v-col cols="12" lg="6">
                           <v-card-text class="mt-12">
                              <h4 class="text-center text-h5">Crie uma conta</h4>
                              <h6 class="text-center grey--text text-subtitle-2">Comece digitando as suas credenciais
                              </h6>
                              <v-row align="center" justify="center">
                                 <v-col cols="12" sm="8">
                                    <v-text-field label="Nome" outlined dense color="primary_green_color" autocomplete="false"
                                       append-inner-icon="mdi-account" class="mt-4" :rules="rule.name" />
                                    <v-text-field label="Email" outlined dense color="primary_green_color" autocomplete="false"
                                       append-inner-icon="mdi-email" :rules="rule.email" />
                                    <v-text-field class="password-field" label="Senha" dense color="primary_green_color"
                                       autocomplete="false" clearable v-model="login.password" :rules="rule.password"
                                       :type="utils.showPassword ? 'text' : 'password'">
                                       <template v-slot:append-inner>
                                          <v-icon @click="toggleShowPassword">
                                             {{ utils.showPassword ? 'mdi-eye' : 'mdi-eye-off' }}
                                          </v-icon>
                                       </template>
                                    </v-text-field>
                                    <v-text-field class="password-field" label="Confirme Senha" dense color="primary_green_color"
                                       autocomplete="false" clearable v-model="utils.confirmPassword"
                                       :type="utils.showConfirmPassword ? 'text' : 'password'">
                                       <template v-slot:append-inner>
                                          <v-icon @click="toggleShowPassword('confirmPassword')">
                                             {{ utils.showConfirmPassword ? 'mdi-eye' : 'mdi-eye-off' }}
                                          </v-icon>
                                       </template>
                                    </v-text-field>
                                    <v-checkbox label="Eu concordo com os termos" color="primary_green_color" :rules="[v => !!v || 'Você deve concordar para prosseguir*']"></v-checkbox>
                                    <v-btn class="mb-10" color="primary_green_color" rounded="1" dark block tile>Registrar-se</v-btn>

                                 
                                    
                                    <div class="d-flex justify-space-around align-center mx-16 mb-16">
                                       <v-btn depressed outlined variant="tonal" class="rounded-circle icons__rounded">
                                          <v-icon color="blue">mdi-facebook</v-icon>
                                       </v-btn>
                                       <v-btn depressed outlined variant="tonal" class="rounded-circle icons__rounded">
                                          <v-icon color="red">mdi-google</v-icon>
                                       </v-btn>
                                       <v-btn depressed outlined variant="tonal" class="rounded-circle icons__rounded">
                                          <v-icon color="light-blue lighten-3">mdi-twitter</v-icon>
                                       </v-btn>
                                    </div>
                                   

                                 </v-col>
                              </v-row>
                           </v-card-text>
                        </v-col>
                     </v-row>
                  </v-window-item>
               </v-window>
            </v-card>
         </v-col>
      </v-row>
   </v-container>
</template>

<script>

import { email, name, password } from '@/composables/rules'

//TOAST
import { toastify } from '@/composables/toast'

export default {
   data: function () {
      return {
         step: 1,
         recoveryLogin: null,
         login: { 'email': null, 'password': null, 'remember': false },
         register: { 'name': null, 'email': null, 'password': null, 'terms': false },
         utils: { 'isFormValid': false, 'showPassword': false, 'showConfirmPassword': false, 'forgotPassword': false, 'loader': false, 'confirmPassword': null, },
         rule: { email, name, password }
      }
   },
   methods: {
      toggleShowPassword: function (event) {
         if (event == "confirmPassword") {
            this.utils.showConfirmPassword = !this.utils.showConfirmPassword;
         } else {
            this.utils.showPassword = !this.utils.showPassword;
         }
      },
      sendEmailToRecoveryPassword: function () {
         this.utils.loader = true;

         axios.post('/api/v1/user/sendEmailToRecoveryPassword',
            { email: this.recoveryLogin },
            { headers: { 'Content-Type': 'application/json' } }
         ).then(() => {
            toastify('success', 'Recuperação de senha solicitada');
         }).catch((error) => {
            if (error.response) {
               const { status, data } = error.response;
               if (status >= 500) {
                  toastify('error', data.message || 'Erro no servidor');
               } else if (status >= 400) {
                  toastify('error', data.message || 'Erro na solicitação');
               } else {
                  toastify('error', 'Erro desconhecido: ' + status);
               }
            } else {
               toastify('error', error.toString());
            }
         }).finally(() => {
            this.utils.loader = false;
            this.utils.forgotPassword = false;
         });
      }

   }


}
</script>
<style scoped>
.card__info {
   height: 100%;
   position: absolute;
   display: flex;
   justify-content: center;
   align-items: center;
}

.card__login {
   background-color: rgba(0, 0, 0, 0.8);
   margin-right: 12px !important;
}

.card__register {
   background-color: rgba(0, 0, 0, 0.8);
   margin-left: 12px !important;
}

.icons__rounded {
   height: 64px !important;
   width: 64px !important;
}

@media (max-width: 1280px) {
   .card__info {
      position: relative !important;
   }

   .card__login {
      margin-right: 0px !important;
   }

   .card__register {
      margin-left: 0px !important;
   }
}

.v-application .rounded-bl-xl {
   border-bottom-left-radius: 300px !important;
}

.v-application .rounded-br-xl {
   border-bottom-right-radius: 300px !important;
}
</style>