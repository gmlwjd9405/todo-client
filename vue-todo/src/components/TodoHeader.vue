// component 당 template 안에 들어가는 HTML tag는 무조건 하나, child 형태로 아래에 추가 
<template>
<header>
    <h1>TODO it!</h1>
</header>
</template>

<script>
export default {

}
</script>

<style scoped>
h1 {
    color: #2F2852;
    font-weight: 900;
    margin: 2.5rem 0 1.5rem; /* 바깥여백 */
}
</style>
