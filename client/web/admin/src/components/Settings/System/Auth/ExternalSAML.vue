<template>
  <div>
    <b-form-group>
      <b-form-checkbox
        v-model="value.enabled"
        :value="true"
        :unchecked-value="false"
      >
        {{ $t('enabled') }}
      </b-form-checkbox>
    </b-form-group>

    <b-form-group
      :label="$t('name')"
      :description="$t('desc.name')"
      label-class="text-primary"
    >
      <b-input-group>
        <b-form-input v-model.trim="value.name" />
      </b-input-group>
    </b-form-group>

    <hr>

    <h5>
      {{ $t('certificate') }}
    </h5>

    <b-form-group
      :label="$t('cert.public')"
      :description="$t('desc.cert.public')"
      label-class="text-primary"
    >
      <b-input-group>
        <b-form-textarea
          v-model.trim="value.cert"
        />
      </b-input-group>
    </b-form-group>
    <b-form-group
      :label="$t('cert.private')"
      :description="$t('desc.cert.private')"
      label-class="text-primary"
    >
      <b-input-group>
        <b-form-textarea v-model.trim="value.key" />
      </b-input-group>
    </b-form-group>

    <hr>

    <h5>
      {{ $t('requests.title') }}
    </h5>

    <b-form-group
      :description="$t('desc.requests.sign-requests')"
    >
      <b-form-checkbox
        v-model="value['sign-requests']"
      >
        {{ $t('requests.sign-requests') }}
      </b-form-checkbox>
    </b-form-group>

    <b-form-group
      :label="$t('requests.sign-method')"
      :description="$t('desc.requests.sign-method')"
      label-class="text-primary"
    >
      <b-input-group>
        <b-form-select
          v-model.trim="value['sign-method']"
          :options="signMethods"
        >
          <template #first>
            <b-form-select-option
              value=""
              disabled
            >
              {{ $t('admin:general.label.selectOption') }}
            </b-form-select-option>
          </template>
        </b-form-select>
      </b-input-group>
    </b-form-group>

    <b-form-group
      :label="$t('requests.binding')"
      :description="$t('desc.requests.binding')"
      label-class="text-primary"
    >
      <b-input-group>
        <b-form-select
          v-model.trim="value['binding']"
          :options="httpBindings"
        >
          <template #first>
            <b-form-select-option
              value=""
              disabled
            >
              {{ $t('admin:general.label.selectOption') }}
            </b-form-select-option>
          </template>
        </b-form-select>
      </b-input-group>
    </b-form-group>

    <hr>

    <h5>
      {{ $t('idp.title') }}
    </h5>

    <b-form-group
      :label="$t('idp.url')"
      :description="$t('desc.idp.url')"
      label-class="text-primary"
    >
      <b-input-group>
        <b-form-input v-model.trim="value.idp.url" />
      </b-input-group>
    </b-form-group>

    <b-form-group
      :label="$t('idp.ident-name')"
      :description="$t('desc.idp.ident-name')"
      label-class="text-primary"
    >
      <b-input-group>
        <b-form-input v-model.trim="value.idp['ident-name']" />
      </b-input-group>
    </b-form-group>

    <b-form-group
      :label="$t('idp.ident-handle')"
      :description="$t('desc.idp.ident-handle')"
      label-class="text-primary"
    >
      <b-input-group>
        <b-form-input v-model.trim="value.idp['ident-handle']" />
      </b-input-group>
    </b-form-group>

    <b-form-group
      :label="$t('idp.ident-identifier')"
      :description="$t('desc.idp.ident-identifier')"
      label-class="text-primary"
    >
      <b-input-group>
        <b-form-input v-model.trim="value.idp['ident-identifier']" />
      </b-input-group>
    </b-form-group>

    <security
      v-model="value.security"
    />
  </div>
</template>
<script>
import Security from './ExternalSecurity'

export default {
  name: 'SamlExternalAuthProvider',

  i18nOptions: {
    namespaces: 'system.settings',
    keyPrefix: 'editor.external.saml',
  },

  components: {
    Security,
  },

  props: {
    value: {
      type: Object,
      required: true,
      default: () => ({}),
    },
  },

  data () {
    return {
      signMethods: [
        { value: 'http://www.w3.org/2000/09/xmldsig#rsa-sha1', text: 'SHA1' },
        { value: 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256', text: 'SHA256' },
        { value: 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha512', text: 'SHA512' },
      ],
      httpBindings: [
        { value: 'urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST', text: this.$t('requests.binding-post') },
        { value: 'urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect', text: this.$t('requests.binding-redirect') },
      ],
    }
  },

}
</script>
<style scoped lang="scss">
</style>
