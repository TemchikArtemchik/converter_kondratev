<template>
    <Page>
        <ActionBar title="Время" />
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
                    <Label class="value" :text="second" row="1" col="0" />
                    <Label class="value" text="с" row="1" col="1" />
                    <Label class="value" :text="minute" row="2" col="0" />
                    <Label class="value" text="мин" row="2" col="1" />
                    <Label class="value" :text="hour" row="3" col="0" />
                    <Label class="value" text="ч" row="3" col="1" />
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
                currentValue: "с",
                second: "",
                minute: "",
                hour: ""
            };
        },
        methods: {
            clear() {
                this.textFieldValue = "";
                this.second = "";
                this.minute = "";
                this.hour = "";
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
                        case "с": {
                            this.second = parseFloat(this.textFieldValue);
                            this.minute = parseFloat(this.textFieldValue) /
                            60;
                            this.hour = parseFloat(this.textFieldValue) /
                            3600;
                            break;
                        }
                        case "мин": {
                            this.second = parseFloat(this.textFieldValue) *
                            60;
                            this.minute = parseFloat(this.textFieldValue);
                            this.hour = parseFloat(this.textFieldValue) / 60;
                            break;
                        }
                        case "ч": {
                            this.second = parseFloat(this.textFieldValue) *
                                3600;
                            this.minute = parseFloat(this.textFieldValue) *
                            60;
                            this.hour = parseFloat(this.textFieldValue);
                            break;
                        }
                        default: {
                            break;
                        }
                    }
                } else {
                    this.second = "";
                    this.minute = "";
                    this.hour = "";
                }
            },
            selectValue() {
                action("Выберите единицу измерения", "Отменить", [
                    "с",
                    "мин",
                    "ч"
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