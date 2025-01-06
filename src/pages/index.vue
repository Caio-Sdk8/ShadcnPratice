<script setup lang='ts'>
import { Button } from '@/components/ui/button'
import { toast } from 'vue-sonner'
import {
  Card,
  CardContent,
  CardDescription,
  CardFooter,
  CardHeader,
  CardTitle,
} from '@/components/ui/card'
import { Input } from '@/components/ui/input'
import { Label } from '@/components/ui/label'
import {
  Select,
  SelectContent,
  SelectItem,
  SelectTrigger,
  SelectValue,
} from '@/components/ui/select'
</script>

<template>
  <div class="container flex items-center justify-center h-screen w-screen">
    <Card class="w-[350px] h-[330px] bg-nosferatu">
      <CardHeader>
        <CardTitle class="text-cullen">Login</CardTitle>
        <CardDescription class="text-cullen">Faça Login para acessar nossa aplicação</CardDescription>
      </CardHeader>
      <CardContent>
        <form>
          <div class="grid items-center w-full gap-4">
            <div class="flex flex-col space-y-1.5">
              <Label for="email" class="text-cullen">E-mail</Label>
              <Input type="email" id="email" placeholder="E-mail" class="text-vonCount" />
            </div>
            <div class="flex flex-col space-y-1.5">
              <Label for="senha" class="text-cullen">Senha</Label>
              <Input type="password" id="senha" placeholder="Senha" class="text-vonCount"/>
            </div>
          </div>
        </form>
      </CardContent>
      <CardFooter class="flex justify-center px-6 pb-6">
        <Button @click="() => {
          toast('Usuário logado com sucesso', {
              description: 'Seja bem vindo a nossa aplicação',
              action: {
                label: 'Desfazer',
                onClick: () => console.log('Desfazer'),
              },
            })
          }">Entrar</Button>
      </CardFooter>
    </Card>
  </div>
</template>