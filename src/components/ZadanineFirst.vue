<script setup>
import { ref,computed} from 'vue';

        let taskBtn = ref(false)
        const taskBtnText = computed(()=>{
            return taskBtn.value ? 'Скрыть условие':'Показать условие'
        })

        const productArr = ref([
      { name: 'Книга', price: 500, quantity: 2 },
      { name: 'Ручка', price: 50, quantity: 5 },
      { name: 'Тетрадь', price: 80, quantity: 3 }])
      console.log(productArr)

        const totalPrice = computed(()=>{
            return productArr.value.reduce((acc,obj)=>{
                return acc + (obj.price*obj.quantity)
            },0)
        })
        const itemsCount = computed(()=>{
            return productArr.value.reduce((acc,obj)=>{
                return acc + obj.quantity
            },0)
        })
        const expensiveItems = computed(()=>{
            return productArr.value.filter(obj=>obj.price>100)
        })
        console.log(totalPrice.value)
        console.log(itemsCount.value)
        console.log(expensiveItems.value)
        
        let calculations = ref(false)
</script>

<template>

    <div class="task" v-show="taskBtn">
        Задача 1 — Корзина покупок (computed)<br><br>
        Дан массив товаров в корзине:<br>
[
            { name: 'Книга', price: 500, quantity: 2 },
            { name: 'Ручка', price: 50, quantity: 5 },
            { name: 'Тетрадь', price: 80, quantity: 3 }
        ]<br><br>
        Создайте:
        computed-свойство totalPrice — считает общую сумму корзины (price × quantity для каждого товара, всё вместе).<br>
        computed-свойство itemsCount — считает общее количество товаров (сумма всех quantity).<br>
        computed-свойство expensiveItems — возвращает массив товаров, у которых price > 100.<br><br>
        Выведите все три значения в шаблон.
    </div>
    <button class="taskBtn" @click="taskBtn=!taskBtn">
        {{ taskBtnText}}
    </button>
    <div class="cards-container">
        <div class="cards-container__card" v-for="product in productArr" :key="product.name">
            <h1>{{ product.name }}</h1>
            <p>Цена {{ product.price }}</p>
            <p>Количество <input type="number" v-model="product.quantity"></p>
        </div>
    </div>
    <button id="calcBtn" @click="calculations=!calculations">Показать расчёты</button>
    <div class="calculations-container" v-show="calculations">
        <p>Общая сумма корзины = {{ totalPrice }} ₽</p>
        <p>Количество товаров в корзине = {{ itemsCount }} шт</p>
        <p v-for="item in expensiveItems" :key='item.name'>
            Товар с ценой выше 100 ₽: {{ item.name }} - {{ item.price}} ₽
        </p>
    </div>


</template>

<style scoped>
    .task{
        width: 70%;
        border: 1px solid black;
        padding: 20px;
        line-height: 110%;
        margin: 30px auto 0;
    }
    .taskBtn{
        display: block;
        width: 150px;
        margin: 30px auto 30px;
        cursor: pointer;
    }
    .cards-container{
        width: 90%;
        padding: 20px;
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        justify-content: center;
        justify-items: center;
        margin: 0 auto;
        row-gap: 20px;
    }
    .cards-container__card{
        border: 2px solid black;
        padding: 30px;
        background-color: #9bdff0;
        border-radius: 10px;
    }
    .cards-container__card>p>input{
        width: 25px;
    }
    #calcBtn{
        display: block;
        width: 150px;
        margin: 30px auto 30px;
        cursor: pointer;
    }
    .calculations-container{
        display: flex;
        flex-direction: column;
        align-items: center;
    }
</style>
