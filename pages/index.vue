<template>
  <div style="min-height: calc(100vh - 64px); padding-top: env(safe-area-inset-bottom);">
  <v-container class="py-5 w-100">
    <v-row class="py-10 text-center">
      <v-col>
        <v-card color="primary" class="py-5" rounded>
          <h1 class="text-h2 font-weight-bold text-white">Gerador de CPF Online Grátis</h1>
        </v-card>
      </v-col>
    </v-row>

    <v-card variant="outlined">
      <v-tabs v-model="tab" align-tabs="center" color="primary">
        <v-tab :value="1">Gerador</v-tab>
        <v-tab :value="2">Validador</v-tab>
      </v-tabs>
      <v-divider></v-divider>
      <v-window v-model="tab">
      
        <v-window-item
          :key="1"
          :value="1"
        >
          <v-container class="py-10">
            <v-row style="max-width: 400px;" class="mx-auto">
              <v-col cols="12">
                <v-text-field 
                  v-model="cpf" 
                  variant="outlined" 
                  label="CPF Válido" 
                  size="large"
                  hide-details="auto"
                  readonly
                  :rules="[(value) => (!value || checkCPF(value)) || 'CPF Inválido.']">
                </v-text-field>
              </v-col>
              <v-col cols="12">
                <v-checkbox hide-details="auto" v-model="isMasked" @change="maskUnmaskCPF()" label="Com máscara"></v-checkbox>
              </v-col>
              <v-row style="max-width: 400px;" class="mx-auto">
                <v-col>
                  <v-btn color="primary" @click="setCpf()" rounded block size="large" append-icon="mdi-refresh">Gerar CPF Válido</v-btn>
                </v-col>
              </v-row>
              <v-col cols="12" class="text-body-2 text-center">
                <p><strong>Clique no botão</strong> para gerar um novo CPF válido</p>
              </v-col>
            </v-row>
          </v-container>
        </v-window-item>


        <v-window-item
          :key="2"
          :value="2"
        >
          <v-container class="py-10">
            <v-row style="max-width: 400px;" class="mx-auto">
              <v-col cols="12">
                <v-text-field 
                  v-model="cpfCheckInput" 
                  variant="outlined" 
                  label="CPF Válido" 
                  size="large"
                  hide-details="auto"
                  :rules="[
                    (value) => (value && value.length >= 11) || 'CPF precisa ter pelo menos 11 digitos.',
                    (value) => checkCPF(value)]
                  ">
                </v-text-field>
              </v-col>
              <v-col cols="12" v-if="cpfCheckInput.length >= 11">
                <v-alert v-if="checkCPF(cpfCheckInput)" color="success">
                  CPF Válido!
                </v-alert>
                <v-alert v-else color="error">
                  CPF Inválido.
                </v-alert>
              </v-col>
              <v-col cols="12" class="text-body-2 text-center">
                <p><strong>Preencha o campo</strong> com um número de CPF para <strong>checar se é válido</strong></p>
              </v-col>
            </v-row>
          </v-container>
        </v-window-item>
      
      </v-window>
    </v-card>

    <v-divider class="my-10"></v-divider>
    <v-row>
      <v-col cols="12">
        <h2 clas="subtitle"><v-icon class="mr-2" color="primary" icon="mdi-chat-question"></v-icon>Perguntas Frequentes:</h2>
      </v-col>
      <v-col cols="12">
        <v-expansion-panels>
          <v-expansion-panel
            v-for="i in faqItems"
            :key="i"
            title="Item"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat."
          ></v-expansion-panel>
        </v-expansion-panels>

      </v-col>
    </v-row>

    <v-row>
      <v-col cols="12">
        <h2 class="subtitle"><v-icon class="mr-2" color="primary" icon="mdi-newspaper-variant-multiple"></v-icon> Artigos Relacionados:</h2>
      </v-col>
    </v-row>
    <v-row>
      <v-col v-for="article of articles" cols="12">
        <v-card variant="outlined" color="primary" :title="article.title" :text="article.description" link :to="article._path"></v-card>
      </v-col>
    </v-row>

  </v-container>
  </div>
</template>
<script lang="ts" setup>
import generateCPF, { checkCPF, unmaskCPF, maskCPF } from '../utils/generateCPF';

const faqItems = ref([]);
const tab = ref(1);
const cpf = ref('');
const cpfCheckInput = ref('');
const isMasked = ref(true);

const setCpf = () => {
  cpf.value = generateCPF(isMasked.value);
};

const maskUnmaskCPF = () => {
  cpf.value = isMasked.value ? maskCPF(cpf.value) : unmaskCPF(cpf.value);
};

const articles = await queryContent('artigos').find();

onMounted(() => {
  setCpf();
})
</script>