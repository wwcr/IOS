<template>
    <div class="header">
        <slot>
            <a v-if="$store.state.header.leftShow" @click="$store.state.header.left" class="go_return"></a>
            <p class="title">{{$store.state.title}}</p>
            <a class="right_btn"
               v-if="$store.state.header.right"
               @click="$store.state.header.rightTouch()">
                    {{$store.state.header.rightContent}}
                <!--<img src="../../assets/img/img_46.jpg">-->
            </a>
        </slot>
    </div>
</template>