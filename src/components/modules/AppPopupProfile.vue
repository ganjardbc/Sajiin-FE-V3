<template>
    <div id="App" style="position: relative;">
        <div 
            :class="`card-small-profile ${visiblePopup ? 'router-link-active' : ''}`" 
            style="height: 40px;"
            @click="visiblePopup = !visiblePopup">
            <div 
                class="image" 
                style="text-align: center; width: 40px; height: 40px;">
                <img 
                    v-if="dataUser && dataUser.image" 
                    :src="dataUser && dataUser.image ? (adminImageThumbnailUrl + dataUser.image) : ''" 
                    alt="">
                <i 
                    v-else 
                    class="post-top fa fa-lg fa-user-circle" 
                    style="color: #999;" />
            </div>
        </div>

        <div 
            v-if="visiblePopup" 
            class="card-profile-menu">
            <div class="card-popup micro no-padding bg-white box-shadow">
                <div style="padding: 15px;">
                    <div style="padding-bottom: 10px;">
                        <AppListInfoMenu 
                            :data.sync="menus" 
                            :onClick="() => visiblePopup = !visiblePopup"
                        />
                    </div>

                    <div class="border-top" style="padding-top: 15px;">
                        <div
                            :class="`card-small-profile display-flex align-center`" 
                            style="height: 40px; cursor: default;">
                            <div 
                                class="image" 
                                style="text-align: center; width: 40px; height: 40px; margin-right: 10px;">
                                <img 
                                    v-if="dataUser && dataUser.image" 
                                    :src="dataUser && dataUser.image ? (adminImageThumbnailUrl + dataUser.image) : ''" 
                                    alt="">
                                <i 
                                    v-else 
                                    class="post-top fa fa-lg fa-user-circle" 
                                    style="color: #999;" />
                            </div>
                            <div style="width: calc(100% - 50px);">
                                <div class="fonts fonts-10 semibold black">{{ dataUser && dataUser.name }}</div>
                                <div class="fonts fonts-10 black">{{ dataUser && dataUser.email }}</div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import AppListInfoMenu from './AppListInfoMenu'

const menus = [
    {icon: 'fa fa-lg fa-user', label: 'User Profile', link: 'profile', permission: 'profile'},
    {icon: 'fa fa-lg fa-user', label: 'Employee Profile', link: 'admin-employee-form', permission: 'employeeform'},
    {icon: 'fa fa-lg fa-calendar-alt', label: 'Reports', link: '404', permission: 'reports'},
]

export default {
    name: 'App',
    data() {
        return {
            visiblePopup: false,
            isSidebarSmall: false,
            menus: menus,
        }
    },
    props: {
        dataUser: {
            default: null 
        },
        notif: {
            required: true 
        }
    },
    components: {
        AppListInfoMenu
    }
}
</script>