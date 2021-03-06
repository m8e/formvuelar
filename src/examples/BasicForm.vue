<!-- Basic form example -->
<template>
  <div class="mt-16">
    <h3 class="border-b-2 mb-4 -mx-4 p-1 text-grey-darkest">
      Basic Form
      <a
        class="float-right text-grey-dark hover:text-teal text-xs no-underline"
        href="https://github.com/janiskelemen/formvuelar/blob/master/src/examples/BasicForm.vue"
        target="_blank"
      >Full Source Code</a>
    </h3>
    <!-- Setup basic form -->
    <fvl-form :data="form" class="relative" url="/basic">
      <!-- Add source code toggle button (only for example) -->
      <source-toggle @toggle="toggleSource('name')"/>
      <!-- Text input component -->
      <fvl-input
        :value.sync="form.name"
        autocomplete="name"
        label="Name"
        name="name"
        placeholder="Type your name"
        type="text"
      />
      <!-- Source code area (only for example) -->
      <source-box :show-source="showSource == 'name'" :source="source.name"/>
      <!-- Add source code toggle button (only for example) -->
      <source-toggle @toggle="toggleSource('text')"/>
      <!-- Textarea component -->
      <fvl-textarea
        :value.sync="form.text"
        label="Text"
        name="text"
        placeholder="Type your story..."
      />
      <!-- Source code area (only for example) -->
      <source-box :show-source="showSource == 'text'" :source="source.text"/>
      <!-- Add source code toggle button (only for example) -->
      <source-toggle @toggle="toggleSource('password')"/>
      <!-- Password input component with custom strength meter -->
      <fvl-input
        :value.sync="form.password"
        autocomplete="new-password"
        class="w-full lg:w-1/2 relative"
        field-class="pr-8"
        label="Password"
        name="password"
        placeholder="Type password"
        type="password"
      >
        <!-- Optional password strength meter using the hint slot -->
        <template slot="hint">
          <div class="absolute pin-r pin-t mt-11 mr-4">
            <transition name="slide-down">
              <span v-if="form.password.length > 0 && form.password.length < 6">😔</span>
              <span v-if="form.password.length >= 6 && form.password.length < 10">😌</span>
              <span v-if="form.password.length >= 10 && form.password.length < 15">😃</span>
              <span v-if="form.password.length >= 15">😍</span>
            </transition>
          </div>
        </template>
      </fvl-input>
      <!-- Source code area (only for example) -->
      <source-box :show-source="showSource == 'password'" :source="source.password"/>
      <!-- Add source code toggle button (only for example) -->
      <source-toggle @toggle="toggleSource('color')"/>
      <!-- Select component -->
      <fvl-select
        :allow-empty="true"
        :options="{'#ffffff': 'White', '#000000': 'Black', 'blue': 'Blue', 'red': 'Red'}"
        :selected.sync="form.color"
        class="w-full lg:w-1/2"
        label="Select your favorite color"
        name="color"
        placeholder="-- Select any color --"
      />
      <!-- Source code area (only for example) -->
      <source-box :show-source="showSource == 'color'" :source="source.color"/>
      <!-- Add source code toggle button (only for example) -->
      <source-toggle @toggle="toggleSource('option')"/>
      <!-- Radio component with options -->
      <fvl-radio
        :checked.sync="form.option"
        :options="{'opt1': 'Option 1', 'opt2': 'Option 2', 'opt3': 'Option 3'}"
        class="w-full lg:w-1/2"
        label="Select any option"
        name="option"
      />
      <!-- Source code area (only for example) -->
      <source-box :show-source="showSource == 'option'" :source="source.option"/>
      <!-- Add source code toggle button (only for example) -->
      <source-toggle @toggle="toggleSource('agree')"/>
      <!-- Checkbox component -->
      <fvl-checkbox
        :checked.sync="form.agree"
        class="w-full lg:w-1/2"
        label="I agree with your terms of use"
        name="agree"
      />
      <!-- Source code area (only for example) -->
      <source-box :show-source="showSource == 'agree'" :source="source.agree"/>
      <!-- Submit button component -->
      <fvl-submit>Validate</fvl-submit>
    </fvl-form>
  </div>
</template>

<script>
  import { FvlForm, FvlInput, FvlTextarea, FvlCheckbox, FvlRadio, FvlSelect, FvlSubmit } from './../formvuelar'

  import SourceToggle from './utilities/SourceToggle.vue'
  import SourceBox from './utilities/SourceBox.vue'

  export default {
    components: {
      FvlForm,
      FvlInput,
      FvlTextarea,
      FvlCheckbox,
      FvlRadio,
      FvlSelect,
      FvlSubmit,
      SourceToggle,
      SourceBox
    },
    data() {
      return {
        form: {
          name: '',
          text: '',
          password: '',
          color: '',
          option: '',
          agree: false
        },
        showSource: '',
        source: {
          name:
            `<fvl-input \n` +
            `     label="Name" \n` +
            `     name="name" \n` +
            `     type="text"  \n` +
            `     autocomplete="name"  \n` +
            `     :value.sync="form.name"  \n` +
            `     placeholder="Type your name"  \n` +
            `/>`,
          text:
            `<fvl-textarea \n` +
            `     label="Text" \n` +
            `     name="text" \n` +
            `     :value.sync="form.text" \n` +
            `     placeholder="Type your story..." \n` +
            `/>`,
          password:
            `<fvl-input \n` +
            `    label="Password" \n` +
            `    name="password" \n` +
            `    type="password" \n` +
            `    autocomplete="new-password" \n` +
            `    :value.sync="form.password" \n` +
            `    placeholder="Type password" \n` +
            `    class="w-1/2 relative" \n` +
            `    fieldClass="pr-8" \n` +
            `> \n` +
            `    <!-- Optional Password Meter --> \n` +
            `    <template slot="hint"> \n` +
            `    <div class="absolute pin-r pin-t mt-12 mr-4"> \n` +
            `        <span v-if="form.password.length > 0 &&  \n` +
            `                    form.password.length < 6">😔</span> \n` +
            `        <span v-if="form.password.length >= 6 &&  \n` +
            `                    form.password.length < 10">😌</span> \n` +
            `        <span v-if="form.password.length >= 10 &&  \n` +
            `                    form.password.length < 15">😃</span> \n` +
            `        <span v-if="form.password.length >= 15">😍</span> \n` +
            `    </div> \n` +
            `    </template> \n` +
            `</fvl-input> \n`,
          color:
            `<fvl-select \n` +
            `    label="Select your favorite color" \n` +
            `    name="color" \n` +
            `    placeholder="-- Select any color --" \n` +
            `    :allowEmpty="true" \n` +
            `    :options="{'#ffffff': 'White', '#000000': 'Black', 'blue': 'Blue', 'red': 'Red'}" \n` +
            `    :checked.sync="form.color" \n` +
            `    class="w-1/2" \n` +
            `/> \n`,
          option:
            `<fvl-radio \n` +
            `    label="Select any option" \n` +
            `    name="option" \n` +
            `    :options="{'opt1': 'Option 1', 'opt2': 'Option 2', 'opt3': 'Option 3'}" \n` +
            `    :checked.sync="form.option" \n` +
            `/> \n`,

          agree:
            `<fvl-checkbox \n` +
            `    label="I agree with your terms of use" \n` +
            `    name="agree" \n` +
            `    :checked.sync="form.agree" \n` +
            `/>`
        }
      }
    },
    methods: {
      toggleSource(field) {
        this.showSource = this.showSource == field ? '' : field
      }
    }
  }
</script>