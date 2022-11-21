<template>
    <Page>
        <ActionBar title="Объем" />
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
                    <Label class="value" :text="milliliter" row="1" col="0" />
                    <Label class="value" text="мл" row="1" col="1" />
                    <Label class="value" :text="liter" row="2" col="0" />
                    <Label class="value" text="л" row="2" col="1" />
                    <Label class="value" :text="cubic_meter" row="3"
                        col="0" />
                    <Label class="value" text="м³" row="3" col="1" />
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
                currentValue: "мл",
                liter: "",
                milliliter: "",
                cubic_meter: ""
            };
        },
        methods: {
            clear() {
                this.textFieldValue = "";
                this.liter = "";
                this.milliliter = "";
                this.cubic_meter = "";
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
                        case "мл": {
                            this.milliliter = parseFloat(this.textFieldValue);
                            this.liter = parseFloat(this.textFieldValue) /
                                1000;
                            this.cubic_meter =
                                parseFloat(this.textFieldValue) / 1000000;
                            break;
                        }
                        case "л": {
                            this.milliliter =
                                parseFloat(this.textFieldValue) * 1000;
                            this.liter = parseFloat(this.textFieldValue);
                            this.cubic_meter =
                                parseFloat(this.textFieldValue) / 1000;
                            break;
                        }
                        case "м³": {
                            this.milliliter =
                                parseFloat(this.textFieldValue) * 1000000;
                            this.liter = parseFloat(this.textFieldValue) *
                                1000;
                            this.cubic_meter = parseFloat(this
                            .textFieldValue);
                            break;
                        }
                        default: {
                            break;
                        }
                    }
                } else {
                    this.liter = "";
                    this.milliliter = "";
                    this.cubic_meter = "";
                }
            },
            selectValue() {
                action("Выберите единицу измерения", "Отменить", [
                    "мл",
                    "л",
                    "м³"
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