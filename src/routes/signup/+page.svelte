<script lang="ts">
    import Card from "../Card.svelte";
    import MultilineInput from "../MultilineInput.svelte";

    let offset: [number, number] = [0, 0];
</script>

<main>
    <svg class="lights" width="787" height="642" viewBox="0 0 787 642" fill="none" xmlns="http://www.w3.org/2000/svg">
        <g filter="url(#filter0_f_0_1)">
        <rect width="449.058" height="15.3322" transform="matrix(0.31838 -0.947963 0.933914 0.357498 527.363 534.519)" fill="url(#paint0_linear_0_1)"/>
        </g>
        <g filter="url(#filter1_f_0_1)">
        <rect width="449.058" height="15.3322" transform="matrix(0.31838 -0.947963 0.933914 0.357498 102 534.519)" fill="url(#paint1_linear_0_1)"/>
        </g>
        <g filter="url(#filter2_f_0_1)">
        <rect width="449.058" height="15.3322" transform="matrix(0.31838 -0.947963 0.933914 0.357498 326.408 534.519)" fill="url(#paint2_linear_0_1)"/>
        </g>
        <g filter="url(#filter3_f_0_1)">
        <rect width="449.058" height="15.3322" transform="matrix(0.31838 -0.947963 0.933914 0.357498 213.939 527.69)" fill="url(#paint3_linear_0_1)"/>
        </g>
        <g filter="url(#filter4_f_0_1)">
        <rect width="449.058" height="15.3322" transform="matrix(0.31838 -0.947963 0.933914 0.357498 438.346 527.69)" fill="url(#paint4_linear_0_1)"/>
        </g>
        <defs>
        <filter id="filter0_f_0_1" x="425.363" y="6.82812" width="361.289" height="635.172" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
        <feFlood flood-opacity="0" result="BackgroundImageFix"/>
        <feBlend mode="normal" in="SourceGraphic" in2="BackgroundImageFix" result="shape"/>
        <feGaussianBlur stdDeviation="51" result="effect1_foregroundBlur_0_1"/>
        </filter>
        <filter id="filter1_f_0_1" x="0" y="6.82812" width="361.289" height="635.172" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
        <feFlood flood-opacity="0" result="BackgroundImageFix"/>
        <feBlend mode="normal" in="SourceGraphic" in2="BackgroundImageFix" result="shape"/>
        <feGaussianBlur stdDeviation="51" result="effect1_foregroundBlur_0_1"/>
        </filter>
        <filter id="filter2_f_0_1" x="224.408" y="6.82812" width="361.289" height="635.172" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
        <feFlood flood-opacity="0" result="BackgroundImageFix"/>
        <feBlend mode="normal" in="SourceGraphic" in2="BackgroundImageFix" result="shape"/>
        <feGaussianBlur stdDeviation="51" result="effect1_foregroundBlur_0_1"/>
        </filter>
        <filter id="filter3_f_0_1" x="111.939" y="0" width="361.289" height="635.172" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
        <feFlood flood-opacity="0" result="BackgroundImageFix"/>
        <feBlend mode="normal" in="SourceGraphic" in2="BackgroundImageFix" result="shape"/>
        <feGaussianBlur stdDeviation="51" result="effect1_foregroundBlur_0_1"/>
        </filter>
        <filter id="filter4_f_0_1" x="336.346" y="0" width="361.289" height="635.172" filterUnits="userSpaceOnUse" color-interpolation-filters="sRGB">
        <feFlood flood-opacity="0" result="BackgroundImageFix"/>
        <feBlend mode="normal" in="SourceGraphic" in2="BackgroundImageFix" result="shape"/>
        <feGaussianBlur stdDeviation="51" result="effect1_foregroundBlur_0_1"/>
        </filter>
        <linearGradient id="paint0_linear_0_1" x1="225.051" y1="-0.00734173" x2="225.04" y2="15.3325" gradientUnits="userSpaceOnUse">
        <stop stop-color="white" stop-opacity="0"/>
        <stop offset="0.5" stop-color="#9B9B9B" stop-opacity="0.13"/>
        <stop offset="1" stop-color="white" stop-opacity="0"/>
        </linearGradient>
        <linearGradient id="paint1_linear_0_1" x1="225.051" y1="-0.00734173" x2="225.04" y2="15.3325" gradientUnits="userSpaceOnUse">
        <stop stop-color="white" stop-opacity="0"/>
        <stop offset="0.5" stop-color="#9B9B9B" stop-opacity="0.13"/>
        <stop offset="1" stop-color="white" stop-opacity="0"/>
        </linearGradient>
        <linearGradient id="paint2_linear_0_1" x1="225.051" y1="-0.00734173" x2="225.04" y2="15.3325" gradientUnits="userSpaceOnUse">
        <stop stop-color="white" stop-opacity="0"/>
        <stop offset="0.5" stop-color="#9B9B9B" stop-opacity="0.13"/>
        <stop offset="1" stop-color="white" stop-opacity="0"/>
        </linearGradient>
        <linearGradient id="paint3_linear_0_1" x1="225.051" y1="-0.00734173" x2="225.04" y2="15.3325" gradientUnits="userSpaceOnUse">
        <stop stop-color="white" stop-opacity="0"/>
        <stop offset="0.5" stop-color="#9B9B9B" stop-opacity="0.13"/>
        <stop offset="1" stop-color="white" stop-opacity="0"/>
        </linearGradient>
        <linearGradient id="paint4_linear_0_1" x1="225.051" y1="-0.00734173" x2="225.04" y2="15.3325" gradientUnits="userSpaceOnUse">
        <stop stop-color="white" stop-opacity="0"/>
        <stop offset="0.5" stop-color="#9B9B9B" stop-opacity="0.13"/>
        <stop offset="1" stop-color="white" stop-opacity="0"/>
        </linearGradient>
        </defs>
    </svg>        
    
    <div class="container">
        <button class="square" style="color:var(--gray12);margin-bottom:8px;">
            <svg width="19" height="21" viewBox="0 0 19 21" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M0.888889 16.5378L8.61111 12.0757V21H10.3889V12.0757L18.1111 16.5378L19 14.9761L11.3056 10.5139L19 6.05179L18.1111 4.49004L10.3889 8.95219V0H8.61111V8.95219L0.888889 4.49004L0 6.05179L7.69444 10.5139L0 14.9761L0.888889 16.5378Z" fill="currentColor"/>
            </svg>                  
        </button>
        <h1>✨ Create your account</h1>
        <p>If you already have an account, you will be signed in automatically.</p>
        <button class="action" style="margin-top: 8px;">
            <svg width="16" height="16" viewBox="0 0 16 16" fill="none" xmlns="http://www.w3.org/2000/svg">
                <g clip-path="url(#clip0_441_37)">
                <path d="M15.04 8.16601C15.04 7.64602 14.9934 7.14602 14.9066 6.66602H8V9.50601H11.9466C11.7734 10.4194 11.2534 11.1926 10.4734 11.7126V13.5594H12.8534C14.24 12.2794 15.04 10.3994 15.04 8.16601Z" fill="#161616"/>
                <path d="M7.99979 15.3338C9.97976 15.3338 11.6398 14.6804 12.8531 13.5604L10.4731 11.7138C9.81976 12.1538 8.98648 12.4204 7.99979 12.4204C6.09312 12.4204 4.47312 11.1338 3.89312 9.40039H1.45312V11.2938C2.65979 13.687 5.13312 15.3338 7.99979 15.3338Z" fill="#161616"/>
                <path d="M3.89464 9.39289C3.74797 8.95289 3.6613 8.48625 3.6613 7.99955C3.6613 7.51289 3.74797 7.04623 3.89464 6.60623V4.71289H1.45464C0.954638 5.69955 0.667969 6.81289 0.667969 7.99955C0.667969 9.18625 0.954638 10.2995 1.45464 11.2862L3.35464 9.80625L3.89464 9.39289Z" fill="#161616"/>
                <path d="M7.99979 3.58602C9.07976 3.58602 10.0398 3.95935 10.8065 4.67935L12.9065 2.57935C11.6331 1.39268 9.97976 0.666016 7.99979 0.666016C5.13312 0.666016 2.65979 2.31268 1.45312 4.71268L3.89312 6.60602C4.47312 4.87268 6.09312 3.58602 7.99979 3.58602Z" fill="#161616"/>
                </g>
                <defs>
                <clipPath id="clip0_441_37">
                <rect width="16" height="16" fill="white"/>
                </clipPath>
                </defs>
            </svg>                            
            Continue with Google
        </button>
    </div>

    <Card position={[4, 4]} size={["500px", "250px"]} bind:offset={offset}>
        <img src="https://creatorspace.imgix.net/users/cle5e0fjh0000mt0yeh5krcpy/DDN4rzgFJl1zcONw-Fa7OYw0XoAAbrfA.jpeg?w=750&h=750" alt="" draggable="false">
    </Card>

    <Card position={[4, 15]} size={["500px", "fit-content"]} bind:offset={offset}>
        <MultilineInput placeholder="Write something cool here"></MultilineInput>
    </Card>

    <Card position={[25, 4]} size={["300px", "175px"]} bind:offset={offset}>
        <div style="padding:24px;width:100%;height:100%;display:flex;flex-direction:column;gap:6px;">
            <div style="width:40px;height:40px;border-radius:12px;border:1px solid var(--gray6);margin-bottom:8px;display:flex;align-items:center;justify-content:center;">
                <img style="width:20px;height:16px;" src="https://storage.googleapis.com/creatorspace-public/sites%2Ffavicons%2FaHR0cHM6Ly9tZXNoLmFhcnYubWUvZmF2aWNvbi5wbmc%3D.png" alt="">
            </div>
            <p style="font-family:Inter;font-size:14px;font-weight:600;color:var(--gray12);width:100%;word-wrap:break-word;">Mesh — Create beautiful SVG gradients</p>
            <p style="font-family:Inter;font-size:12px;color:var(--gray11);">mesh.aarv.me</p>
        </div>
    </Card>

    <Card position={[25, 12]} size={["300px", "325px"]} style="youtube" bind:offset={offset}>
        <div style="padding:24px;width:100%;height:100%;display:flex;flex-direction:column;gap:6px;">            
            <div style="width:40px;height:40px;border-radius:12px;display:flex;align-items:center;justify-content:center;margin-bottom:8px;box-shadow:0 1px 2px rgb(0 0 0 / 10%);">
                <svg width="40" height="400" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg"><rect width="40" height="40" rx="10" fill="#FF0000"></rect><path fill-rule="evenodd" clip-rule="evenodd" d="M29.3766 12.5016C30.4093 12.7775 31.2225 13.5907 31.4986 14.6233L31.4985 14.6234C32 16.495 32 20.4001 32 20.4001C32 20.4001 32 24.305 31.4985 26.1768C31.2224 27.2094 30.4092 28.0225 29.3765 28.2986C27.505 28.8 19.9999 28.8 19.9999 28.8C19.9999 28.8 12.4949 28.8 10.6233 28.2986C9.59065 28.0224 8.77727 27.2094 8.50144 26.1767C8 24.3049 8 20.4 8 20.4C8 20.4 8 16.4949 8.50144 14.6233C8.77727 13.5907 9.59065 12.7775 10.6234 12.5016C12.495 12 20 12 20 12C20 12 27.5051 12 29.3766 12.5016ZM24.4429 20.6931L17.6001 24.5857V16.8L24.4429 20.6931Z" fill="white"></path></svg>              
            </div>
            <p style="font-family:Inter;font-size:14px;font-weight:600;color:var(--gray12);width:100%;word-wrap:break-word;">Illusions of Time</p>
            <p style="font-family:Inter;font-size:12px;color:var(--gray11);">By Vsauce</p>

            <div style="width:fit-content;height:fit-content;margin-top:auto;position:relative;">
                <img draggable="false" style="border-radius:12px;user-select:none;height:100%;" src="data:image/jpeg;base64,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" alt="">
                <div style="position:absolute;width:fit-content;height:fit-content;background-color:rgba(0, 0, 0, 0.6);bottom:8px;right:8px;border-radius:4px;color:white;font-size:11px;font-weight:500;font-family:Inter;padding:2px 4px;">
                    31:08
                </div>
            </div>
        </div>
    </Card>

    <Card position={[38, 4]} size={["300px", "400px"]} style="twitter" bind:offset={offset}>
        <div style="width:100%;height:100%;padding:24px;display:flex;flex-direction:column;gap:8px;">
            <div style="width:40px;height:40px;border-radius:12px;display:flex;align-items:center;justify-content:center;margin-bottom:8px;box-shadow:0 1px 2px rgb(0 0 0 / 10%);">
                <svg width="40" height="40" viewBox="0 0 40 40" fill="none" xmlns="http://www.w3.org/2000/svg"><rect width="40" height="40" rx="10" fill="#55ACEE"></rect><mask id="mask0_920_2751" maskUnits="userSpaceOnUse" x="8" y="10" width="24" height="20" style="mask-type: luminance;"><path d="M31.9309 10.2326H8V29.6807H31.9309V10.2326Z" fill="white"></path></mask><g mask="url(#mask0_920_2751)"><path d="M31.9309 12.5347C31.0506 12.9253 30.1043 13.1891 29.1112 13.3078C30.1248 12.7002 30.9034 11.7381 31.27 10.5915C30.3211 11.1543 29.2704 11.5628 28.152 11.7829C27.2565 10.8287 25.9806 10.2326 24.5684 10.2326C21.857 10.2326 19.6586 12.4307 19.6586 15.1421C19.6586 15.5269 19.702 15.9017 19.7858 16.261C15.7053 16.0563 12.0876 14.1016 9.66603 11.1312C9.24342 11.8563 9.00123 12.6996 9.00123 13.5994C9.00123 15.3028 9.86801 16.8056 11.1854 17.686C10.3806 17.6605 9.62356 17.4396 8.96163 17.0719C8.96107 17.0924 8.96107 17.113 8.96107 17.1337C8.96107 19.5124 10.6535 21.4967 12.8995 21.948C12.4876 22.0602 12.0538 22.1202 11.606 22.1202C11.2897 22.1202 10.9822 22.0893 10.6823 22.032C11.3071 23.9826 13.1203 25.4021 15.2688 25.4416C13.5885 26.7585 11.4716 27.5434 9.17118 27.5434C8.77489 27.5434 8.38409 27.5201 8 27.4747C10.1728 28.8679 12.7535 29.6807 15.5262 29.6807C24.5569 29.6807 29.4955 22.1995 29.4955 15.7113C29.4955 15.4985 29.4906 15.2868 29.4813 15.0761C30.4404 14.384 31.2727 13.5194 31.9309 12.5347Z" fill="white"></path></g></svg>
            </div>

            <p style="font-family:Inter;font-size:14px;color:var(--gray12);">
                <span style="font-weight:600;">Aarav Sareen</span>
                <span style="color:var(--gray11);">@arvsrn</span>
            </p>
            <p style="font-family:Inter;font-size:14px;color:var(--gray12);">Create beautiful SVG gradients → http://mesh.aarv.me</p>

            <img draggable="false" style="border-radius:12px;user-select:none;margin-top:auto;" src="https://pbs.twimg.com/media/Fke80u_VsAA9o7j?format=jpg&name=small" alt="">
        </div>
    </Card>
</main>

<style>
    main {
        width: 100vw;
        height: 100vh;

        background: #161616;

        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    div.container {
        display: flex;
        flex-direction: column;
        gap: 8px;

        box-sizing: content-box;
        width: 333px;
        height: fit-content;

        padding: 24px;
        border-radius: 12px;

        backdrop-filter: blur(5px);
        z-index: 100;
    }

    svg.lights {
        position: absolute;

        left: 50%;
        top: 50%;

        transform: translate(-50%, -50%);
        pointer-events: none;
    }

    button.square {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;

        color: var(--gray11);
        
        width: 40px;
        height: 40px;

        background-color: var(--gray2);
        border: 1px solid var(--gray5);
        outline: none;
        border-radius: 12px;
        
        cursor: pointer;
        transition: transform 0.1s ease-in-out;
    }

    button.square:hover {
        transform: scale(1.05);
    }

    button.square:active {
        transform: scale(1);
    }

    h1, p {
        width: 100%;
        height: fit-content;

        word-wrap: break-word;
    }

    h1 {
        font-family: 'Inter';
        font-style: normal;
        font-weight: 700;
        font-size: 14px;
        line-height: 17px;

        color: #EDEDED;
    }

    p {
        font-family: 'Inter';
        font-style: normal;
        font-weight: 400;
        font-size: 14px;
        line-height: 17px;

        color: #A0A0A0;
    }

    button.action {
        width: 100%;
        height: 48px;

        background: #EDEDED;
        border-radius: 12px;

        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        padding: 10px;
        gap: 6px;

        font-family: 'Inter';
        font-style: normal;
        font-weight: 600;
        font-size: 14px;
        line-height: 17px;

        color: #161616;

        outline: none;
        border: none;
        cursor: pointer;
        transition: transform 0.1s ease-in-out;
    }

    button.action:hover {
        transform: scale(1.03);
    }

    button.action:active {
        transform: scale(0.98);
    }
</style>