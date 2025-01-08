<script setup lang="ts">
import { Label } from '@/components/ui/label'
import { RadioGroup, RadioGroupItem } from '@/components/ui/radio-group'
</script>

<template>
  <RadioGroup class="flex h-[40px] w-[300px] text-cullen justify-evenly" default-value="comfortable">
    <div class="flex items-center space-x-2">
      <RadioGroupItem class="border-white bg-white" id="r1" value="default" />
      <Label for="r1">Masculino</Label>
    </div>
    <div class="flex items-center space-x-2">
      <RadioGroupItem class="border-white bg-white" id="r2" value="comfortable" />
      <Label for="r2">Feminino</Label>
    </div>
    <div class="flex items-center space-x-2">
      <RadioGroupItem class="border-white bg-white" color="primary" id="r3" value="compact" />
      <Label for="r3">Outros</Label>
    </div>
  </RadioGroup>
</template>