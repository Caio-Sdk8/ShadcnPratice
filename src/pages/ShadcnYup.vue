<script setup lang="ts">
import { Button } from "@/components/ui/button";
import {
  FormControl,
  FormDescription,
  FormField,
  FormItem,
  FormLabel,
  FormMessage,
} from "@/components/ui/form";
import {
  Card,
  CardContent,
  CardDescription,
  CardFooter,
  CardHeader,
  CardTitle,
} from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { toast } from "vue-sonner";
import { vAutoAnimate } from "@formkit/auto-animate/vue";
import { useForm } from "vee-validate";
import * as Yup from "yup";
import { h } from "vue";

import DatePicker from "../components/SingIn/DatePicker.vue";
import RadioGroup from "../components/SingIn/RadioGroup.vue";

const formSchema = Yup.object({
  name: Yup.string()
    .min(2, "O nome deve possuir ao menos 2 caracteres.")
    .max(50, "O nome deve possuir no máximo 50 caracteres.")
    .required("Nome é obrigatório."),
  email: Yup.string()
    .email("E-mail inválido.")
    .min(3, "O e-mail deve possuir ao menos 3 caracteres.")
    .max(180, "O e-mail deve possuir no máximo 180 caracteres.")
    .required("E-mail é obrigatório."),
  password: Yup.string()
    .min(8, "A senha deve possuir ao menos 8 caracteres.")
    .matches(/[A-Z]/, "A senha deve conter ao menos uma letra maiúscula.")
    .matches(/[a-z]/, "A senha deve conter ao menos uma letra minúscula.")
    .matches(/[0-9]/, "A senha deve conter ao menos um número.")
    .matches(/[@$!%*?&#]/, "A senha deve conter ao menos um caractere especial.")
    .required("Senha é obrigatória."),
  confirmPassword: Yup.string()
    .oneOf([Yup.ref("password"), undefined], "As senhas devem coincidir.")
    .required("Confirmação de senha é obrigatória."),
});

const { handleSubmit } = useForm({
  validationSchema: formSchema,
});

const onSubmit = handleSubmit((values) => {
  toast({
    title: "Você enviou os seguintes valores:",
    description: h(
      "pre",
      { class: "mt-2 w-[340px] rounded-md bg-slate-950 p-4" },
      h(
        "code",
        { class: "text-white" },
        JSON.stringify(values, null, 2)
      )
    ),
  });
});
</script>

<template>
  <div class="container flex items-center justify-center h-screen w-screen">
    <Card class="mt-8 w-[350px] h-[720px] bg-nosferatu">
      <CardHeader>
        <CardTitle class="text-cullen">Cadastro</CardTitle>
        <CardDescription class="text-cullen">
          Faça cadastro para acessar nossa aplicação
        </CardDescription>
      </CardHeader>
      <CardContent>
        <form @submit.prevent="onSubmit">
          <div class="grid items-center w-full gap-4">
            <div class="flex flex-col space-y-1.5">
              <FormField v-slot="{ componentField }" name="name">
                <FormItem v-auto-animate>
                  <FormLabel class="text-cullen">Nome</FormLabel>
                  <FormControl>
                    <Input
                      type="text"
                      placeholder="Nome"
                      class="text-vonCount"
                      v-bind="componentField"
                    />
                  </FormControl>
                  <FormMessage />
                </FormItem>
              </FormField>
            </div>
            <div class="flex flex-col space-y-1.5">
              <FormField v-slot="{ componentField }" name="email">
                <FormItem v-auto-animate>
                  <FormLabel class="text-cullen">E-mail</FormLabel>
                  <FormControl>
                    <Input
                      type="email"
                      placeholder="E-mail"
                      class="text-vonCount"
                      v-bind="componentField"
                    />
                  </FormControl>
                  <FormMessage />
                </FormItem>
              </FormField>
            </div>
            <div class="flex flex-col space-y-1.5">
              <Label class="text-cullen">Data de Nascimento</Label>
              <DatePicker />
            </div>
            <div class="flex flex-col space-y-1.5">
              <Label class="text-cullen">Gênero</Label>
              <RadioGroup />
            </div>
            <div class="flex flex-col space-y-1.5">
              <FormField v-slot="{ componentField }" name="password">
                <FormItem v-auto-animate>
                  <FormLabel class="text-cullen">Senha</FormLabel>
                  <FormControl>
                    <Input
                      type="password"
                      placeholder="Senha"
                      class="text-vonCount"
                      v-bind="componentField"
                    />
                  </FormControl>
                  <FormMessage />
                </FormItem>
              </FormField>
            </div>
            <div class="flex flex-col space-y-1.5">
              <FormField v-slot="{ componentField }" name="confirmPassword">
                <FormItem v-auto-animate>
                  <FormLabel class="text-cullen">Confirme sua Senha</FormLabel>
                  <FormControl>
                    <Input
                      type="password"
                      placeholder="Confirmação de senha"
                      class="text-vonCount"
                      v-bind="componentField"
                    />
                  </FormControl>
                  <FormMessage />
                </FormItem>
              </FormField>
            </div>
          </div>
        </form>
      </CardContent>
      <CardFooter class="flex justify-center px-6 pb-6">
        <Button class="mt-4" @click="() => {
          toast('Usuário Cadastrado com sucesso', {
              description: 'Seja bem vindo a nossa aplicação',
              action: {
                label: 'Desfazer',
                onClick: () => console.log('Desfazer'),
              },
            })
          }">Cadastrar</Button>
      </CardFooter>
    </Card>
  </div>
</template>