<template>
    <v-container>
        <v-row justify="center">
            <v-col v-for="country in favoriteCountries" v-bind:key="country" cols="12" sm="12" md="6" lg="4" xl="3">
                <CountryCard v-bind:country="country">
                    <template v-slot:cardTop="{countryInfo}">
                        <v-card-title style="text-align: center">
                            {{ countryInfo.translations?.[localeMap[$i18n.locale]]?.official || countryInfo.name.official }}
                        </v-card-title>
                    </template>
                </CountryCard>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
import CountryCard from '@/components/CountryCard.vue';
import { mapState, mapActions } from 'vuex';

export default {
    components: {
        CountryCard
    },
    data() {
        return {
            localeMap: {
                en: "eng",
                ru: "rus",
                ar: "ara"
            }
        }
    },
    methods: {
        ...mapActions({
            removeCountryFromFavorites: "FavoriteCountries/changeCountryFavoriteState"
        })
    },
    computed: {
        ...mapState({
            favoriteCountries: state => state.FavoriteCountries.favoriteCountries
        })
    }
}
</script>