<template>
  <form @submit.prevent="submit">
    <div class="block general">
      <div class="group contatInfo">
        <h2>Представьтесь, пожалуйста</h2>
        <InputText
          :title="'Фамилия'"
          :id="'lastName'"
          :isRequired="true"
          :isValid="isValidLastName"
          :errorMessage="getErrorMessage('lastName')"
          @changed="changeValue($event, 'lastName')"
        />
        <InputText
          :title="'Имя'"
          :id="'firstName'"
          :isRequired="true"
          :isValid="isValidFirstName"
          :errorMessage="getErrorMessage('firstName')"
          @changed="changeValue($event, 'firstName')"
        />
        <InputText
          :title="'Организация и должность'"
          :id="'organization'"
          :isRequired="false"
          :isValid="isValidOrganization"
          :errorMessage="getErrorMessage('organization')"
          @changed="changeValue($event, 'organization')"
        />
        <Radio
          :selectedData="positionData"
          :groupName="'position'"
          @changed="changeValue($event, 'position')"
        />
      </div>
      <div class="group messageBlock">
        <h2>Сообщение</h2>
        <InputText
          :title="'Тема сообщения'"
          :id="generateId()"
          :isRequired="false"
          :isValid="isValidMessageCaption"
          :errorMessage="getErrorMessage('messageCaption')"
          @changed="changeValue($event, 'messageCaption')"
        />
        <TextArea
          :id="generateId()"
          :isRequired="true"
          :isValid="isValidMessage"
          :errorMessage="getErrorMessage('message')"
          @changed="changeValue($event, 'message')"
          :title="'Сообщение'"
        />
      </div>
    </div>
    <div class="block userData">
      <div class="group contactInformation">
        <h2>Контактная информация</h2>
        <InputText
          :title="'Email'"
          :id="generateId()"
          :isRequired="true"
          :isValid="isValidEmail"
          :errorMessage="getErrorMessage('email')"
          @changed="changeValue($event, 'email')"
        />
        <InputText
          :title="'Страна'"
          :id="generateId()"
          :isRequired="false"
          :isValid="isValidCountry"
          :errorMessage="getErrorMessage('country')"
          @changed="changeValue($event, 'country')"
        />
        <InputText
          :title="'Город'"
          :id="generateId()"
          :isRequired="false"
          :isValid="isValidCity"
          :errorMessage="getErrorMessage('city')"
          @changed="changeValue($event, 'city')"
        />
        <InputText
          :title="'Индекс'"
          :id="generateId()"
          :isRequired="false"
          :isValid="isValidIndex"
          :errorMessage="getErrorMessage('index')"
          @changed="changeValue($event, 'index')"
        />
        <InputText
          :title="'Адрес'"
          :id="generateId()"
          :isRequired="false"
          :isValid="isValidAddress"
          :errorMessage="getErrorMessage('address')"
          @changed="changeValue($event, 'address')"
        />
        <InputText
          :title="'Телефон'"
          :id="generateId()"
          :isRequired="true"
          :isValid="isValidPhone"
          :placeholder="'(___)___-__-__'"
          :errorMessage="getErrorMessage('phone')"
          @changed="changeValue($event, 'phone')"
        />
        <button type="submit">Отправить</button>
      </div>
    </div>
  </form>
</template>

<script>
import InputText from "@/components/controls/InputText";
import Radio from "@/components/controls/Radio";
import TextArea from "@/components/controls/TextArea";

export default {
  components: {
    Radio,
    InputText,
    TextArea,
  },
  data() {
    return {
      isValidFirstName: true,
      isValidLastName: true,
      isValidMessage: true,
      isValidEmail: true,
      isValidCountry: true,
      isValidCity: true,
      isValidIndex: true,
      isValidMessageCaption: true,
      isValidPhone: true,
      isValidOrganization: true,
      isValidAddress: true,
      firstName: "",
      lastName: "",
      organization: "",
      position: "",
      messageCaption: "",
      message: "",
      email: "",
      country: "",
      city: "",
      index: "",
      address: "",
      phone: "",
      positionData: [
        { id: this.generateId(), isDefault: true, title: "Потребитель" },
        {
          id: this.generateId(),
          isDefault: false,
          title: "Медицинский работник",
        },
        { id: this.generateId(), isDefault: false, title: "Журналист" },
      ],
    };
  },
  methods: {
    submit() {
      this.isValidFirstName =
        this.cyrillicValidate(this.firstName) &&
        this.requiredValidate(this.firstName);
      this.isValidLastName =
        this.cyrillicValidate(this.lastName) &&
        this.requiredValidate(this.lastName);
      this.isValidOrganization =
        this.cyrillicValidate(this.organization) ||
        !this.requiredValidate(this.organization);
      this.isValidCountry =
        this.cyrillicValidate(this.country) ||
        !this.requiredValidate(this.country);
      this.isValidCity =
        this.cyrillicValidate(this.city) || !this.requiredValidate(this.city);
      this.isValidMessageCaption =
        this.cyrillicWithNumberValidate(this.messageCaption) ||
        !this.requiredValidate(this.messageCaption);
      this.isValidMessage =
        this.cyrillicWithNumberValidate(this.messageCaption) &&
        this.requiredValidate(this.messageCaption);
      this.isValidAddress =
        this.addressValidate(this.address) ||
        !this.requiredValidate(this.address);
      this.isValidPhone =
        this.phoneValidate(this.phone) && this.requiredValidate(this.phone);
      this.isValidIndex =
        this.indexValidate(this.index) || !this.requiredValidate(this.index);
      this.isValidEmail =
        this.emailValidate(this.email) && this.requiredValidate(this.email);
      if (this.isValidForm()) {
        alert("valid");
      } else {
        alert("error");
      }
    },
    changeValue($event, prop) {
      this[prop] = $event;
    },
    generateId() {
      return (Math.random() + 1).toString(36).substring(7);
    },
    cyrillicValidate(value) {
      return /^[\u0400-\u04FF|\s]+$/.test(value);
    },
    cyrillicWithNumberValidate(value) {
      return /^[\u0400-\u04FF|\d|\s]+$/.test(value);
    },
    addressValidate(address) {
      return /^[\u0400-\u04FF|\d|/|.|,|\s]+$/.test(address);
    },
    phoneValidate(phone) {
      return /^(\+)?(38)?(\()?\d{3}(\))?\d{2}(-)?\d{2}(-)?\d{3}$/.test(phone);
    },
    requiredValidate(value) {
      return Boolean(value.toString().trim());
    },
    indexValidate(index) {
      return /^\d{6}$/.test(index);
    },
    emailValidate(email) {
      return /^[\w-.]+@([\w-]\+.)+[\w-]{2,4}$/.test(email);
    },
    getErrorMessage(field) {
      const requiredFiels = "Поле обезательное для заполнения";
      switch (field) {
        case "firstName":
        case "lastName":
          return requiredFiels + " и должно содержать только кириллицу";
        case "email":
          return requiredFiels + " и должно содержать корректный email";
        case "phone":
          return requiredFiels + " и должно содержать номер телефона";
        case "message":
          return requiredFiels;
        case "messageCaption":
        case "organization":
        case "country":
        case "city":
          return "Поле должно содерджать только кириллицу";
        case "address":
          return "Поле должно содержать только кириллицу, запятую, точку или '/'";
        case "index":
          return "Поле должно только 6 цифр";
      }
    },
    isValidForm() {
      return (
        this.isValidLastName &&
        this.isValidFirstName &&
        this.isValidAddress &&
        this.isValidMessage &&
        this.isValidEmail &&
        this.isValidCountry &&
        this.isValidCity &&
        this.isValidIndex &&
        this.isValidMessageCaption &&
        this.isValidPhone &&
        this.isValidOrganization
      );
    },
  },
};
</script>

<style scoped>
form {
  width: 80%;
  min-width: 320px;
  margin: 0 auto;
  display: flex;
  gap: 15%;
  justify-content: center;
  flex-wrap: wrap;
}

.block {
  display: flex;
  flex-direction: column;
}

h2 {
  font-weight: 400;
  font-size: 18px;
  text-transform: uppercase;
}

.contactInformation {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

button {
  width: 246px;
  height: 31px;
  background: #464646;
  border: 1px solid #000000;
  box-sizing: border-box;
  font-size: 22px;
  color: #ffffff;
  text-transform: uppercase;
}
</style>
