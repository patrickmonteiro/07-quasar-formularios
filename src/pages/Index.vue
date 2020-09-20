<template>
  <q-page class="container" padding>
    <p class="text-h4">Formulário</p>
      <q-form
        @submit="onSubmit"
        @reset="onReset"
        class="row q-col-gutter-md"
        ref="myForm"
      >
        <q-input
          outlined
          v-model="form.nome"
          color="deep-purple"
          label="Nome"
          class="col-md-12 col-sm-12 col-xs-12"
          :rules="[
            val => val && val.length > 0 ||  'Nome obrigatório'
          ]"
        >
          <template v-slot:prepend>
            <q-icon name="person" />
          </template>
        </q-input>

        <q-input
          v-model.number="form.idade"
          type="number"
          outlined
          label="Idade"
          class="col-md-12 col-sm-12 col-xs-12"
          :rules="[
            val => val !== null && val !== '' || 'Idade obrigatória',
            val => val > 0 && val < 100 || 'Coloque uma idade real'
          ]"
        >
          <template v-slot:prepend>
            <q-icon name="person" />
          </template>
        </q-input>

        <q-input
          v-model="form.email"
          label="Email"
          suffix="@gmail.com"
          outlined
          class="col-md-12 col-sm-12 col-xs-12"
          :rules="[
            val => val && val.length > 0 ||  'Email obrigatório'
          ]"
        >
          <template v-slot:prepend>
            <q-icon name="mails" />
          </template>
        </q-input>

        <q-input
          v-model="form.telefone"
          label="Telefone"
          outlined
          class="col-md-12 col-sm-12 col-xs-12"
          mask="(##) #####-####"
          unmasked-value
          :rules="[
            val => val && val.length > 0 || 'Telefone obrigatório',
            val => val.length === 11 || 'Coloque um telefone real'
          ]"
        />

        <q-select
          outlined
          v-model="form.tipoPessoa"
          :options="optionsTipoPessoa"
          label="Tipo de Pessoa"
          class="col-md-12 col-sm-12 col-xs-12"
          emit-value
          map-options
          :rules="[
            val => val && val.length > 0 || 'Tipo de Pessoa obrigatório'
          ]"
        />
        <span class="text-bold">Sexo:</span>
        <q-option-group
          :options="optionsSexo"
          label="Sexo"
          type="radio"
          v-model="form.sexo"
          class="col-md-12 col-sm-12 col-xs-12"
        />
        <span class="text-bold">Possui alguma dificuldade? </span>
        <q-option-group
          :options="optionsDificuldades"
          label="Dificuldades"
          type="checkbox"
          v-model="form.dificuldades"
          class="col-md-12 col-sm-12 col-xs-12"
        />

        <q-toggle
          v-model="form.notificacoes"
          color="primary"
          icon="mail"
          label="Receber notificações?"
          size="lg"
        />

        <div class="col-12">
          <q-btn
            label="Cadastrar"
            type="submit"
            color="primary"
            class="float-right"
          />
          <q-btn
            label="Resetar"
            type="reset"
            color="default"
            class="float-right text-grey-10 q-mr-md"
          />
        </div>
      </q-form>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      form: {
        nome: '',
        idade: null,
        email: '',
        telefone: '',
        tipoPessoa: '',
        sexo: 'NI',
        dificuldades: [],
        notificacoes: false
      },
      optionsTipoPessoa: [
        { label: 'Pessoa Física', value: 'pf' },
        { label: 'Pessoa Jurídica', value: 'pj' }
      ],
      optionsSexo: [
        { label: 'Não Informado', value: 'NI' },
        { label: 'Masculino', value: 'M' },
        { label: 'Feminino', value: 'F' }
      ],
      optionsDificuldades: [
        { label: 'Motoras', value: 'motoras' },
        { label: 'Visuais', value: 'visuais' },
        { label: 'Respiratórias', value: 'respiratorias' }
      ]
    }
  },
  methods: {
    onSubmit () {
      this.$q.notify({
        message: 'Cadastro realizado com sucesso',
        color: 'positive',
        icon: 'check_circle_outline'
      })
      this.onReset()
    },
    async onReset () {
      await this.resetForm()
      this.$refs.myForm.resetValidation()
    },
    async resetForm () {
      this.form = {
        nome: '',
        idade: null,
        email: '',
        telefone: '',
        tipoPessoa: '',
        sexo: 'NI',
        dificuldades: [],
        notificacoes: false
      }
    }
  }
}
</script>
