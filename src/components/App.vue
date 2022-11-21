<template>
    <Page>
        <ActionBar title="Converter" />
        <ScrollView>
            <GridLayout class="container" columns="*, *" rows="*, *, *">
                <Button @tap="onItemTap('Вес, масса')" row="0"
                    class="containerItem" col="0" text="Вес, масса">
                </Button>
                <Button @tap="onItemTap('Время')" row="0"
                    class="containerItem" col="1" text="Время">
                </Button>
                <Button @tap="onItemTap('Температура')" row="1"
                    class="containerItem" col="0" text="Температура">
                </Button>
                <Button @tap="onItemTap('Длина')" row="1"
                    class="containerItem" col="1" text="Длина">
                </Button>
                <Button @tap="onItemTap('Площадь')" row="2"
                    class="containerItem" col="0" text="Площадь">
                </Button>
                <Button @tap="onItemTap('Объём')" row="2"
                    class="containerItem" col="1" text="Объём">
                </Button>
            </GridLayout>
        </ScrollView>
    </Page>
</template>

<script>
    import Length from "./Length";
    import Weight from "./Weight";
    import Temperature from "./Temperature";
    import Time from "./Time";
    import Area from "./Area";
    import Volume from "./Volume";

    export default {
        components: {
            Length,
            Weight,
            Time,
            Temperature,
            Area,
            Volume
        },
        methods: {
            onItemTap: function(namePage) {
                switch (namePage) {
                    case "Вес, масса": {
                        this.$navigateTo(Weight);
                        break;
                    }
                    case "Время": {
                        this.$navigateTo(Time);
                        break;
                    }
                    case "Температура": {
                        this.$navigateTo(Temperature);
                        break;
                    }
                    case "Длина": {
                        this.$navigateTo(Length);
                        break;
                    }
                    case "Площадь": {
                        this.$navigateTo(Area);
                        break;
                    }
                    case "Объём": {
                        this.$navigateTo(Volume);
                        break;
                    }
                }
            }
        },

        data() {
            return {};
        }
    };
</script>

<style>

    * {
        margin: 0;
        padding: 0;
    }

    ActionBar {
        background-color: #001f63;
        color: white;
        height: 230px;
    }

    Button {
        color: hwb(242 0% 62%);
    }

    GridLayout {
        height: 100%;
    }

    Label {
        font-size: 18;
        text-align: center;
        padding: 20px 15x;
    }

    .value {
        margin: 0px 40px 40px 40px;
        border-radius: 2;
        background-color: white;
    }

    .bt1 {
        padding: 20px 10x;
        margin-bottom: 80px;
        margin-top: 40px;
        border-radius: 2;
        font-size: 18px;
        background-color: white;
    }

    .select {
        width: 30%;
    }

    .btn {
        font-size: 22;
        color: hsl(219, 100%, 19%);
    }

    .container {
        padding: 40px 20px;
        background-color: #E6FFFF;
    }

    .containerItem {
        font-size: 22;
        width: 100%;
        height: 100%;
        color: hsl(206, 100%, 19%);
    }

    .return {
        font-size: 18px;
        margin-bottom: 50px;
    }
</style>