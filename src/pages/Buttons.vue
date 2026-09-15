<script setup>
import Btn from "../components/Btn.vue";
</script>

<template>
    <div class="button-page">
        <div class="page-header">
            <h1 class="title mb-2">Button Playground</h1>
            <p class="subtitle is-6">
                Reusable Bulma buttons with different props
            </p>
        </div>

        <div class="box">
            <h2 class="title is-5">Colors</h2>

            <div class="buttons">
                <Btn color="primary">Primary</Btn>
                <Btn color="info">Info</Btn>
                <Btn color="success">Success</Btn>
                <Btn color="warning">Warning</Btn>
                <Btn color="danger">Danger</Btn>
                <Btn color="dark">Dark</Btn>
            </div>
        </div>

        <div class="box">
            <h2 class="title is-5">Different styles</h2>

            <div class="buttons">
                <Btn color="primary" rounded>
                    Rounded
                </Btn>

                <Btn color="danger" outlined>
                    Outlined
                </Btn>

                <Btn color="info" light>
                    Light
                </Btn>

                <Btn color="success" rounded outlined>
                    Mixed
                </Btn>
            </div>
        </div>

        <div class="box">
            <h2 class="title is-5">Sizes</h2>

            <div class="buttons is-align-items-center">
                <Btn color="info" size="small">
                    Small
                </Btn>

                <Btn color="info">
                    Normal
                </Btn>

                <Btn color="info" size="medium">
                    Medium
                </Btn>

                <Btn color="info" size="large">
                    Large
                </Btn>
            </div>
        </div>

        <div class="box">
            <h2 class="title is-5">States</h2>

            <div class="buttons">
                <Btn color="success" loading>
                    Loading
                </Btn>

                <Btn color="danger" disabled>
                    Disabled
                </Btn>
            </div>
        </div>
    </div>
</template>

<style scoped>
.button-page {
    max-width: 850px;
    margin: 0 auto;
    padding: 30px 15px;
}

.page-header {
    text-align: center;
    margin-bottom: 30px;
}

.box {
    margin-bottom: 20px;
    border-radius: 14px;
}
</style>