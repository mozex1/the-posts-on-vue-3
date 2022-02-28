<template>
    <div class="matrix" >
        <canvas ref="canvas"></canvas>
    </div>
</template>
<script>
export default {
    name: 'my-matrix-screen',
    methods: {
        startAnim() {
            const C = this.$refs.canvas,
            $ = C.getContext("2d"),
            W = (C.width = window.innerWidth),
            H = (C.height = window.innerHeight);

            const str = "П+РИ0Г-ЛА=5СИ2Н 6АЗ С04Й М5Е С6ТИ М5У Р8АТ Т9Т И!М У?Р АТИ.М,У Р:ЭА5;Я",
            matrix = str.split("");

            let font = 11,
            col = W / font,
            arr = [];

            for (let i = 0; i < col; i++) arr[i] = 1;

            function draw() {
                $.fillStyle = "rgba(255,255,255, 0.2)";
                $.fillRect(0, 0, W, H);
                $.fillStyle = "teal";
                $.font = font + "px system-ui";
                for (let i = 0; i < arr.length; i++) {
                    let txt = matrix[Math.floor(Math.random() * matrix.length)];
                    $.fillText(txt, i * font, arr[i] * font);
                    if (arr[i] * font > H && Math.random() > 0.975) arr[i] = 0;
                    arr[i]++;
                }
            }

            setInterval(draw, 123);

            window.addEventListener("resize", () => location.reload());

        }
    },
    mounted() {
        this.startAnim();
    }
}
</script>
<style scoped>
    .matrix {
        margin: 0;
        margin-top: 10px;
        background: white;
        overflow: hidden;
    }
</style>