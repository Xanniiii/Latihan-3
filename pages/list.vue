<template>
    <div class="container">
        <ul>
            <li v-for="item in item" :key="item.message">
                {{ item.message }}
            </li>
        </ul>
    </div>
</template>