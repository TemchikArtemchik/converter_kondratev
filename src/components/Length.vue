<template>
    <Page>
        <ActionBar title="Длина" />
        <ScrollView>
            <StackLayout class="container">
                <Button class="return" text="< Назад" @tap="$navigateBack"/>
                <GridLayout class="value" columns="2*, *"
                    rows="auto, auto, auto, auto, auto" backgroundColor="teal">
                    <TextField class="bt1"
                        v-model="textFieldValue"
                        @textChange="calculationValue(currentValue)"
                        keyboardType="number" hint="Введите значение..."
                        row="0" col="0" />
                    <Button class="bt1" :text="currentValue"
                        @tap="selectValue" row="0" col="1" />
                    <Label class="value" :text="centimeter" row="1" col="0" />
                    <Label class="value" text="см" row="1" col="1" />
                    <Label class="value" :text="meter" row="2" col="0" />
                    <Label class="value" text="м" row="2" col="1" />
                    <Label class="value" :text="kilometer" row="3" col="0" />
                    <Label class="value" text="км" row="3" col="1" />
                    <Label class="value" :text="miles" row="4" col="0" />
                    <Label class="value" text="мили" row="4" col="1" />
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
                currentValue: "см",
                meter: "",
                centimeter: "",
                kilometer: "",
                miles: ""
            };
        },
        methods: {
            clear() {
                this.textFieldValue = "";
                this.meter = "";
                this.centimeter = "";
                this.kilometer = "";
                this.miles = "";
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
                        case "см": {
                            this.centimeter = parseFloat(this.textFieldValue);
                            this.miles = parseFloat(this.textFieldValue) / 160934;
                            this.meter = parseFloat(this.textFieldValue) /
                            100;
                            this.kilometer =
                                parseFloat(this.textFieldValue) / 100000;
                            break;
                        }
                        case "м": {
                            this.centimeter = parseFloat(this
                                .textFieldValue) * 100;
                            this.miles = parseFloat(this.textFieldValue) / 1609.344;
                            this.meter = parseFloat(this.textFieldValue);
                            this.kilometer = parseFloat(this.textFieldValue) / 1000;
                            break;
                        }
                        case "км": {
                            this.centimeter =
                                parseFloat(this.textFieldValue) * 100000;
                            this.meter = parseFloat(this.textFieldValue) *
                                1000;
                            this.miles = parseFloat(this.textFieldValue) / 1.609344;
                            this.kilometer = parseFloat(this.textFieldValue);
                            break;
                        }
                        case "мили": {
                            this.centimeter = parseFloat(this.textFieldValue) * 160934;
                            this.meter = parseFloat(this.textFieldValue) *
                            1609.344;
                            this.miles = parseFloat(this.textFieldValue);
                            this.kilometer = parseFloat(this.textFieldValue) * 1.609344;
                            break;
                        }
                        default: {
                            break;
                        }
                    }
                } else {
                    this.meter = "";
                    this.centimeter = "";
                    this.kilometer = "";
                    this.miles = "" 
                }
            },
            selectValue() {
                action("Выберите единицу измерения", "Отменить", [
                    "см",
                    "м",
                    "км",
                    "мили"
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

<style scoped>

</style>