<script setup lang="ts">
import { Button } from '@/components/ui/button'
import { Calendar } from '@/components/ui/calendar'
import { cn } from '@/lib/utils'
import { Popover, PopoverContent, PopoverTrigger } from '@/components/ui/popover'
import {
  DateFormatter,
  type DateValue,
  getLocalTimeZone,
} from '@internationalized/date'
import { Calendar as CalendarIcon } from 'lucide-vue-next'
import { ref } from 'vue'
import type { DatePicker } from 'radix-vue/namespaced'

const df = new DateFormatter('pt-BR', {
  dateStyle: 'long',
})

const value = ref<DateValue>()
</script>

<template>
  <Popover>
    <PopoverTrigger as-child>
      <Button
        variant="outline"
        :class="cn(
          'w-[300px] h-[40px] justify-start text-left font-normal text-vonCount',
          !value && 'text-muted-foreground',
        )"
      >
        <CalendarIcon class="mr-2 h-4 w-4" />
        {{ value ? df.format(value.toDate(getLocalTimeZone())) : "Selecione uma Data" }}
      </Button>
    </PopoverTrigger>
    <PopoverContent class="w-[300px] p-0">
      <Calendar v-model="value" initial-focus />
    </PopoverContent>
  </Popover>
</template>