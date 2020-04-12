<template>
  <div>
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">

      <b-form-group id="input-group-1" label="Recepient Name:" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model="form.name"
          required
          placeholder="Enter name"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Recepient Title:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.title"
          required
          placeholder="Enter Title"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-3" label="Recepient Industry:" label-for="input-3">
        <b-form-input
          id="input-3"
          v-model="form.industry"
          required
          placeholder="Enter Industry"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-4" label="Company:" label-for="input-4">
        <b-form-input
          id="input-4"
          v-model="form.company"
          required
          placeholder="Enter Company"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-5" label="Email:" label-for="input-5">
        <b-form-input
          id="input-5"
          v-model="form.email"
          required
          placeholder="Enter Email"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-6" label="Type:" label-for="input-6">
        <b-form-select
          id="input-5"
          v-model="form.type"
          :options="types"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group id="input-group-4">
        <b-form-checkbox-group v-model="form.checked" id="checkboxes-4">
          <b-form-checkbox value="me">Check me out</b-form-checkbox>
          <b-form-checkbox value="that">Check that out</b-form-checkbox>
        </b-form-checkbox-group>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
    <b-card class="mt-3 text-left" header="Email Body">
      <pre class="m-0" v-show="this.form.type === 'FollowUp'" v-html="emailtemplate"></pre>
      <pre class="m-0" v-show="this.form.type === 'secondfollowup'" v-html="followuptemplate"></pre>
      <pre class="m-0" v-show="this.form.type === 'lastfollowup'" v-html="finaltemplate"></pre>
    </b-card>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        form: {
          name: '',
          title: '',
          industry: '',
          company: '',
          email: '',
          type: null,
          checked: []
        },
        emailbody: '',
        followupbody: '',
        finalbody: '',
        emailtemplate: '',
        followuptemplate: '',
        finaltemplate: '',
        firstsubject: 'Connecting Like Minds for a Virtual Chat',
        followupsubject: 'Virtual Chat Follow-Up',
        types: [{ text: 'Select One', value: null }, 'FollowUp', 'secondfollowup', 'lastfollowup'],
        show: true
      }
    },
    methods: {
      onSubmit(evt) {
        evt.preventDefault()
        this.emailbody =
        `
        Hi ${this.form.name},I came across your profile on LinkedIn and
        felt compelled to reach out to you. As someone with a desire to
        work as a Software Engineer within the Tech industry, your background in
        the ${this.form.industry} industry and the journey that led you to your
        current role at ${this.form.company} as a ${this.form.title} is
        interesting to me. While this may be a bit forward, I would love to
        virtually connect with you to gain some advice and hear your story. I am
        sure you are quite busy, but even just 30 minutes of your time will give
        me the opportunity to learn from someone with an impressive background
        like your own.

        I know with recent circumstances it will be best to meet over video chat
        or via phone call. I am usually available to meet 6:00 to 9:00 A.M CT and
        12:00-1:00 PM CT on weekdays. Please let me know if there is a timeframe
        that works best for you. Thank you in advance and I’m looking forward to
        hearing back from you!

        Best Regards,
        Adam Shaffer
        `
        this.emailtemplate =
        `
        ${this.emailbody}

        <a href='mailto:${this.form.email}?subject=${this.firstsubject}&body=${this.emailbody}' target='_blank'>EMAIL</a>
        `
        this.followupbody =
        `
        Hi ${this.form.name},

        I am following up on my previous email to see if you are still
        interested connecting. I’d love to learn more about your career journey
        and insights into the tech industry. I’m sure you’re busy so even 20
        minutes would be appreciated. I am available to meet virtually 6:00 to
        9:00 A.M CT and 12:00-1:00 PM CT on weekdays.

        Thanks so much,
        Adam Shaffer.

        `
        this.followuptemplate =
        `
        ${this.followupbody}

        <a href='mailto:${this.form.email}?subject=${this.followupsubject}&body=${this.followupbody}' target='_blank'>EMAIL</a>

        `
        this.finalbody =
        `
        Hi ${this.form.name},

        I am following up on my previous email to see if your are still interested in
        touching base. I am sure you are busy but I would greatly appreciate just
        20 minutes of your time to learn more aobut your career journey and gain insights
        from your experience. If you can make the time feel free to reach out.

        Thanks so much,
        Adam Shaffer.

        `


        this.finaltemplate =
        `
        ${this.followupbody}

        <a href='mailto:${this.form.email}?subject={followupsubject}&body=${this.followupbody}' target='_blank'>EMAIL</a>
        `
      },
      onReset(evt) {
        evt.preventDefault()
        // Reset our form values
        this.form.email = ''
        this.form.name = '',
        this.form.title = ''
        this.form.company = ''
        this.form.type = null
        this.emailtemplate = '',
        this.followuptemplate = '',
        this.finaltemplate = ''
        this.form.checked = []
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  }
</script>
