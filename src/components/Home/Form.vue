<script setup>
import { ref, reactive } from 'vue';

const emit = defineEmits(['closeForm'])
const form = ref()
const isValid = ref(false);
let isValidate = reactive({});


function isValidName(name) {
  // le nom et prénom doivent avoir plus de 3 caractères et ne contenant pas de chiffre
  const regex = /^[a-zA-Z'\-]{3,}$/;
  return regex.test(name);
}

function isValidEmail(email) {
  // L’email doit avoir un format valide
  const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return regex.test(email);
}

function isValidDate(input) {
  let selectDate = new Date(input);
  let age = new Date().getFullYear() - selectDate.getFullYear();
  return age >= 10;
}

function isValidNumber(participation) {
  return participation !== "" &&
      Number.isInteger(Number(participation)) &&
      participation >= 0;
}

function submit(event) {
  const { firstname, lastname, email, birthday, nbParticipation, town, validCondition } = Object.fromEntries(new FormData(event.target));

  if (!isValidName(firstname)) {
    isValidate.firstname = false
    isValidate.firstnameMsg = "Le prénom doit avoir plus de 3 caractères et ne doit pas contenir de chiffres."
  } else {
    isValidate.firstname = true
    isValidate.firstnameMsg = "Champ Valide"
  }

  if (!isValidName(lastname)) {
    isValidate.lastname = false;
    isValidate.lastnameMsg = "Le nom doit avoir plus de 3 caractères et ne doit pas contenir de chiffres."
  } else {
    isValidate.lastname = true;
    isValidate.lastnameMsg = "Champ Valide"

  }

  if (!isValidDate(birthday)) {
    isValidate.birthday = false
    isValidate.birthdayMsg = "Vous devez avoir plus de 10 ans."
  } else {
    isValidate.birthday = true
    isValidate.birthdayMsg = "Champ Valide"

  }

  if (!isValidEmail(email)) {
    isValidate.email = false
    isValidate.emailMsg = "L'e-mail doit avoir un format valide."
  } else {
    isValidate.email = true
    isValidate.emailMsg = "Champ Valide"
  }

  if (typeof town === 'undefined') {
    isValidate.town = false
    isValidate.townMsg = "Veuillez sélectionner au moins une ville.";
  } else {
    isValidate.town = true
    isValidate.townMsg = "Champ Valide"
  }

  if (!isValidNumber(nbParticipation)) {
    isValidate.nbParticipation = false
    isValidate.nbParticipationMsg = "Veuillez renseignez votre nombre de participation."
  } else {
    isValidate.nbParticipation = true;
    isValidate.nbParticipationMsg = "Champ Valide"
  }

  if (typeof validCondition === 'undefined') {
    isValidate.validCondition = false
    isValidate.validConditionMsg = "Veuillez lire et valider les conditions d'utilisation."
  } else {
    isValidate.validCondition = true
    isValidate.validConditionMsg = "Champ Valide"
  }


  if (!Object.entries(isValidate).some((error) => error[1] === false)) {
    isValid.value = true;
    form.value.reset();
  }

}


function formClose() {
  emit('closeForm');
  isValid.value = false;
  form.value.reset();
  isValidate = reactive({});
}

</script>

<template>
  <div class="main__form form">
    <div class="form__close" @click="formClose">
      <i class="fa-solid fa-xmark quit_form"></i>
    </div>
    <form @submit.prevent="(event) => submit(event)" ref="form" id="form" itemscope itemtype="https://schema.org/Person">

      <ul :class="{ form__items: true, displayBlock: !isValid, displayNone: isValid }">
        <li class="form__item">
          <label for="firstname">Prénom</label>
          <input type="text" name="firstname" placeholder="Votre prénom..." id="firstname" itemprop="givenName" />
          <small :class="{ error: !isValidate.firstname, success: isValidate.firstname }">{{ isValidate.firstnameMsg
          }}</small>
        </li>
        <li class="form__item">
          <label for="lastname">Nom</label>
          <input type="text" name="lastname" id="lastname" placeholder="Votre nom..." itemprop="familyName" />
          <small :class="{ error: !isValidate.lastname, success: isValidate.lastname }">{{ isValidate.lastnameMsg
          }}</small>
        </li>
        <li class="form__item">
          <label for="email">E-mail</label>
          <input type="text" name="email" id="email" placeholder="example@mail.com" itemprop="email" />
          <small :class="{ error: !isValidate.email, success: isValidate.email }">{{ isValidate.emailMsg }}</small>

        </li>
        <li class="form__item">
          <label for="birthday">Date de naissance</label>
          <input type="date" name="birthday" id="birthday" itemprop="birthDate" />
          <small :class="{ error: !isValidate.birthday, success: isValidate.birthday }">{{ isValidate.birthdayMsg
          }}</small>

        </li>
        <li class="form__item">
          <label for="nb-participation">À combien de tournois GameOn avez-vous déja participé ?</label>
          <input type="number" name="nbParticipation" id="nbParticipation" placeholder="Nombre de participation..." />
          <small :class="{ error: !isValidate.nbParticipation, success: isValidate.nbParticipation }">{{
            isValidate.nbParticipationMsg }}</small>

        </li>
        <li class="form__item--no">
          <div class="radio">
            <label for="town">À quel tournois souhaitez-vous participer cette année ?</label><br />
            <label for="new-york">New-York</label>
            <input type="radio" name="town" class="town" value="new-york" placeholder="New York" itemprop="memberOf" />
            <label for="sans-francisco">Sans-Francisco</label>
            <input type="radio" name="town" class="town" value="sans-francisco" placeholder="sans-francisco"
              itemprop="memberOf" />
            <label for="seatle">Seatle</label>
            <input type="radio" name="town" class="town" value="seatle" placeholder="seatle" itemprop="memberOf" />
            <label for="chicago">Chicago</label>
            <input type="radio" name="town" class="town" value="chicago" placeholder="chicago" itemprop="memberOf" />
            <label for="boston">Boston</label>
            <input type="radio" name="town" class="town" value="boston" placeholder="boston" itemprop="memberOf" />
            <label for="portland">Portland</label>
            <input type="radio" name="town" class="town" value="portland" placeholder="portland" itemprop="memberOf" />
          </div>
          <small :class="{ error: !isValidate.town, success: isValidate.town }">{{ isValidate.townMsg }}</small>

        </li>
        <li class="form__item--no" itemscope itemtype="https://schema.org/CheckAction">
          <div class="check">
            <input type="checkbox" name="validCondition" id="validCheckbox" placeholder="valid" value="readCondition"
              itemprop="potentialAction" />
            <label for="valid" itemprop="name">J'ai lue et accepté les conditions d'utilisation</label><br />
            <small :class="{ error: !isValidate.validCondition, success: isValidate.validCondition }">{{
              isValidate.validConditionMsg }}</small>

          </div>
          <div>
            <input type="checkbox" name="notification" id="nofification" placeholder="notification"
              value="acceptNotification" itemprop="potentialAction" />
            <label for="notification" itemprop="name">Je souhaite être prévenu des prochains évènement</label>
          </div>
        </li>
        <li class="form__item" itemscope itemtype="https://schema.org/CommunicateAction">
          <button type="submit" class="form__sub-btn btn valid_form" itemprop="potentialAction">Je
            M'inscris</button>
        </li>
      </ul>
    </form>
    <div :class="{ form__success: true, displayBlock: isValid, displayNone: !isValid }" itemscope
      itemtype="https://schema.org/EventReservation">
      <div class="form__success-container">
        <h2 class="form__success-msg">Merci pour votre inscription</h2>
        <button class="form__sub-btn btn quit_form" @click="formClose">Fermer</button>
        <meta itemprop="reservationStatus" content="http://schema.org/Confirmed" />
      </div>
    </div>
  </div>
</template>

<style>
.error {
  color: red;
}

.success {
  color: greenyellow;
}
</style>