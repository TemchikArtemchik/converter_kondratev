<template>
    <Page>
        <ActionBar title="Площадь" />
        <ScrollView>
            <StackLayout class="container">
                <Button class="return" text="< Назад" @tap="$navigateBack" />
                <GridLayout class="value" columns="2*, *"
                    rows="auto, auto, auto, auto" backgroundColor="teal">
                    <TextField class="bt1" v-model="textFieldValue"
                        @textChange="calculationValue(currentValue)"
                        keyboardType="number" hint="Введите значение..."
                        row="0" col="0" />
                    <Button class="bt1" :text="currentValue"
                        @tap="selectValue" row="0" col="1" />
                    <Label class="value" :text="square_meter" row="1"
                        col="0" />
                    <Label class="value" text="м²" row="1" col="1" />
                    <Label class="value" :text="square_kilometer" row="2"
                        col="0" />
                    <Label class="value" text="км²" row="2" col="1" />
                    <Label class="value" :text="square_inch" row="3"
                        col="0" />
                    <Label class="value" text="дюйм²" row="3" col="1" />
                </GridLayout>
            </StackLayout>
        </ScrollView>
    </Page>
</template>

<script>
    export default {
        data() {
            return {
                textFieldValue: "",
                currentValue: "м²",
                square_meter: "",
                square_kilometer: "",
                square_inch: ""
            };
        },
        methods: {
            clear() {
                this.textFieldValue = "";
                this.square_meter = "";
                this.square_kilometer = "";
                this.square_inch = "";
            },
            calculationValue(currentValue) {
                
                if (this.textFieldValue != "") {
                    if (this.textFieldValue == "-") {
                        alert({
                            title: "Ошибка!",
                            message: "Величина не может быть отрицательной.",
                            okButtonText: "ОК"
                        }).then(() => {
                            this.clear()
                        });
                    }
                    if (this.textFieldValue == "." || this.textFieldValue == "+") {
                        alert({
                            title: "Ошибка!",
                            message: "Некорректный ввод.",
                            okButtonText: "ОК"
                        }).then(() => {
                            this.clear()
                        });
                    }
                    switch (currentValue) {
                        case "м²": {
                            this.square_meter = parseFloat(this
                                .textFieldValue);
                            this.square_kilometer =
                                parseFloat(this.textFieldValue) / 1000000;
                            this.square_inch =
                                parseFloat(this.textFieldValue) * 1550;
                            break;
                        }
                        case "км²": {
                            this.square_meter =
                                parseFloat(this.textFieldValue) * 1000000;
                            this.square_kilometer = parseFloat(this
                                .textFieldValue);
                            this.square_inch =
                                parseFloat(this.textFieldValue) * 1550000000;
                            break;
                        }
                        case "дюйм²": {
                            this.square_meter =
                                parseFloat(this.textFieldValue) / 1550;
                            this.square_kilometer =
                                parseFloat(this.textFieldValue) / 1550000000;
                            this.square_inch = parseFloat(this
                            .textFieldValue);
                            break;
                        }
                        default: {
                            break;
                        }
                    }
                } else {
                    this.square_meter = "";
                    this.square_kilometer = "";
                    this.square_inch = "";
                }
            },
            selectValue() {
                action("Выберите единицу измерения", "Отменить", [
                    "м²",
                    "км²",
                    "дюйм²"
                ]).then(result => {
                    if (result != "Отменить") {
                        this.currentValue = result;
                        this.calculationValue(this.currentValue);
                    }
                });
            }
        }
    };
</script>

<style>

</style>