<script setup>
    import { ref,computed} from 'vue';

    let taskBtn2 = ref(false)
        const taskBtnText2 = computed(()=>{
            return taskBtn2.value ? 'Скрыть условие':'Показать условие'
        })
    
    let counter = ref(0)
// Массив из 5000 случайных чисел есть
    const randomNumbersArr = ()=>{
        return Array.from({length:5000},()=>{
            return Math.floor(Math.random()*10000)
        })
    }
    let numbers = ref(randomNumbersArr())
// computed
    const sortedList = computed(()=>{
        console.log('Пересчитано! (Сработал COMPUTED)');
        return [...numbers.value].sort((a,b)=>{
            return a-b
        })
    })
// просто через метод sort
    const sortedListMethod = ()=>{
        console.log('Пересчитано! (Сработал Sort())');
        return [...numbers.value].sort((a,b)=>a-b)}


</script>

<template>

    <div class="task2" v-show="taskBtn2">
        Задача 2 — Computed vs Method (эксперимент)<br><br>
        Создайте одну и ту же логику двумя способами — как computed-свойство sortedList<br> и как метод sortedListMethod() — которая сортирует большой массив (сгенерируйте массив из 5000 случайных чисел).<br>
        Добавьте на страницу кнопку-счётчик, не связанную с массивом <code v-pre>(<button @click="counter++">{{ counter }}</button>)</code>.<br>
        Добавьте в обе функции console.log('Пересчитано!').<br>
        Нажмите кнопку несколько раз и посмотрите в консоль.<br>
        Ответьте письменно (2-3 предложения): что вы увидели в консоли и почему? Какой вариант эффективнее и почему?
    </div>
    <button class="taskBtn2" @click="taskBtn2=!taskBtn2">
        {{ taskBtnText2}}
    </button>
    <button id="counter" @click="counter++">{{ counter }}</button>
    <div class="solution">
        <p>результат сортировки через computed: {{ sortedList.slice(0,15).join(', ') }}...</p>
        <p>результат сортировки метод sort(): {{ sortedListMethod().slice(0,15).join(', ') }}...</p>
        <p>В консоли 1 раз появляется выражение Пересчитано! (Сработал COMPUTED). Т.к. данные отсортированы 1 раз, кэшированы и зависимые величины не меняются.<br>
        А без computed, метод sorted сортирует массив каждый раз при обновлении кнопки. В консоли появится Пересчитано!+counter  Т.к. template рендерится сверху вниз, computed понимает, что данные в массиве не изменились,<br> 
        а метод sort() без computed этого не понимает, т.к. не проверяет кэш. <br>
        Эффективнее computed, т.к. избавляет от лишней нагрузки компьютер. 
        </p>
    </div>
</template>

<style scoped>
    .task2{
        width: 70%;
        border: 1px solid black;
        padding: 20px;
        line-height: 110%;
        margin: 30px auto 0;
    }
    .taskBtn2{
        display: block;
        width: 150px;
        margin: 30px auto 30px;
        cursor: pointer;
    }
    #counter{
        display: block;
        width: 150px;
        margin: 30px auto 30px;
        cursor: pointer;
    }

</style>
