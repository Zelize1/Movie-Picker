<script setup

<template>
    <div>
        <h1>Genres</h1>
        <ul>
            <li v-for="genre in genres" :key="genre.id">
                <router-link :to="{ name: 'genre', params: { id: genre.id } }">{{ genre.name }}</router-link>
            </li>
        </ul>
        
    </div>
</template>