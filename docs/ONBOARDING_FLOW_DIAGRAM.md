# Authentication Flow - Complete Visual Diagram

## New Wallet Creation Flow (First-Time User)

```
┌─────────────────────────────────────────────────────────────┐
│                   APP LAUNCH (First Time)                   │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           v
┌─────────────────────────────────────────────────────────────┐
│                     START SCREEN                            │
│                    (Phase 2 - NEW!)                         │
│  ┌───────────────────────────────────────────────────────┐ │
│  │   [Blockchain Illustration]                           │ │
│  │                                                       │ │
│  │   "Own, control, and leverage the power              │ │
│  │    of your digital assets"                           │ │
│  │                                                       │ │
│  │   ┌──────────────────────────────────────┐           │ │
│  │   │  🎨 Create new wallet                │           │ │
│  │   └──────────────────────────────────────┘           │ │
│  │                                                       │ │
│  │   ┌──────────────────────────────────────┐           │ │
│  │   │  📥 I already have a wallet          │           │ │
│  │   └──────────────────────────────────────┘           │ │
│  │                                                       │ │
│  │   By tapping you agree to ToS...                     │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
│  Analytics: start_screen_shown                             │
│  File: start_screen.dart                                   │
└──────────────────────────┬──────────────────────────────────┘
                           │ "Create new wallet"
                           v
┌─────────────────────────────────────────────────────────────┐
│                  WALLET TYPE SELECTION                      │
│                    (Existing Screen)                        │
│  ┌───────────────────────────────────────────────────────┐ │
│  │   Select wallet type:                                 │ │
│  │   • Iguana Wallet                                     │ │
│  │   • HD Wallet                                         │ │
│  │   • Trezor (Hardware)                                 │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
│  Analytics: onboarding_started(method: 'create')           │
└──────────────────────────┬──────────────────────────────────┘
                           │ Select type
                           v
┌─────────────────────────────────────────────────────────────┐
│               PASSCODE ENTRY (OPTIONAL)                     │
│                    (Phase 2 - NEW!)                         │
│  ┌───────────────────────────────────────────────────────┐ │
│  │   Create passcode                                     │ │
│  │   Enter your passcode. Be sure to remember it...      │ │
│  │                                                       │ │
│  │   ○ ○ ○ ○ ○ ○  ← PIN dots                            │ │
│  │                                                       │ │
│  │   ┌───────────────────┐                               │ │
│  │   │  1    2    3      │                               │ │
│  │   │  4    5    6      │  ← Numeric keypad             │ │
│  │   │  7    8    9      │                               │ │
│  │   │       0    ⌫      │                               │ │
│  │   └───────────────────┘                               │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
│  Analytics: passcode_created                               │
│  File: passcode_entry_screen.dart                          │
│  Service: PasscodeService.setPasscode()                    │
└──────────────────────────┬──────────────────────────────────┘
                           │ 6 digits entered
                           v
┌─────────────────────────────────────────────────────────────┐
│             PASSCODE CONFIRMATION (OPTIONAL)                │
│                    (Phase 2 - NEW!)                         │
│  ┌───────────────────────────────────────────────────────┐ │
│  │   Confirm passcode                                    │ │
│  │   Re-enter your passcode...                           │ │
│  │                                                       │ │
│  │   ● ● ● ● ● ●  ← Filled dots                          │ │
│  │                                                       │ │
│  │   [Same keypad]                                       │ │
│  │                                                       │ │
│  │   ✓ or ✗ Match validation                            │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
│  File: passcode_confirm_screen.dart                        │
│  Validation: Compare with original                         │
└──────────────────────────┬──────────────────────────────────┘
                           │ Passcode confirmed
                           v
┌─────────────────────────────────────────────────────────────┐
│                WALLET CREATION FORM                         │
│                    (Existing Screen)                        │
│  ┌───────────────────────────────────────────────────────┐ │
│  │   Wallet name: [________________]                     │ │
│  │   Password:    [________________]                     │ │
│  │   Confirm:     [________________]                     │ │
│  │   □ HD Wallet Mode                                    │ │
│  │   □ Quick Login                                       │ │
│  │   ☑ I agree to EULA/ToS                               │ │
│  │                                                       │ │
│  │   [Create Wallet]                                     │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
│  File: wallet_creation.dart                                │
└──────────────────────────┬──────────────────────────────────┘
                           │ Submit form
                           v
┌─────────────────────────────────────────────────────────────┐
│               [AUTHBLOC CREATES WALLET]                     │
│             Intercept: Start Seed Backup Flow               │
└──────────────────────────┬──────────────────────────────────┘
                           │ Wallet created
                           v
┌─────────────────────────────────────────────────────────────┐
│               SEED BACKUP WARNING                           │
│                   (Phase 1 - CRITICAL!)                     │
│  ┌───────────────────────────────────────────────────────┐ │
│  │   [Security Illustration]                             │ │
│  │                                                       │ │
│  │   👁  For your eyes only!                             │ │
│  │   This secret phrase unlocks your wallet              │ │
│  │                                                       │ │
│  │   ┌─────────────────────────────────────┐             │ │
│  │   │ 🔑 Komodo wallet does not have      │             │ │
│  │   │    access to this key.              │             │ │
│  │   └─────────────────────────────────────┘             │ │
│  │   ┌─────────────────────────────────────┐             │ │
│  │   │ 📝 Don't save in digital format,    │             │ │
│  │   │    write on paper...                │             │ │
│  │   └─────────────────────────────────────┘             │ │
│  │   ┌─────────────────────────────────────┐             │ │
│  │   │ ⚠️  If you lose your phrase, coins  │             │ │
│  │   │    are lost forever...              │             │ │
│  │   └─────────────────────────────────────┘             │ │
│  │                                                       │ │
│  │   [Continue]                                          │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
│  Analytics: seed_backup_warning_shown                      │
│  File: seed_backup_warning_screen.dart                     │
│  Security: Cannot be skipped                               │
└──────────────────────────┬──────────────────────────────────┘
                           │ Continue
                           v
┌─────────────────────────────────────────────────────────────┐
│                    SEED DISPLAY                             │
│                   (Phase 1 - CRITICAL!)                     │
│  ┌───────────────────────────────────────────────────────┐ │
│  │   Manual backup                                    ✕  │ │
│  │                                                       │ │
│  │   ┌──────────┐  ┌──────────┐                         │ │
│  │   │ 1. aware │  │ 7. noise │                         │ │
│  │   └──────────┘  └──────────┘                         │ │
│  │   ┌──────────┐  ┌──────────┐                         │ │
│  │   │2. envelop│  │8. cushion│                         │ │
│  │   └──────────┘  └──────────┘                         │ │
│  │   ┌──────────┐  ┌──────────┐                         │ │
│  │   │3. regular│  │9. situate│                         │ │
│  │   └──────────┘  └──────────┘                         │ │
│  │   ┌──────────┐  ┌──────────┐                         │ │
│  │   │4. rubber │  │10. cloud │                         │ │
│  │   └──────────┘  └──────────┘                         │ │
│  │   ┌──────────┐  ┌──────────┐                         │ │
│  │   │5. situate│  │11.envelope│                        │ │
│  │   └──────────┘  └──────────┘                         │ │
│  │   ┌──────────┐  ┌──────────┐                         │ │
│  │   │6. toddler│  │12. rubber│                         │ │
│  │   └──────────┘  └──────────┘                         │ │
│  │                                                       │ │
│  │   ⚠️  Never share your secret phrase!                 │ │
│  │                                                       │ │
│  │   [Continue]                                          │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
│  Analytics: seed_displayed                                 │
│  File: seed_display_screen.dart                            │
│  Security: Screenshot protected                            │
└──────────────────────────┬──────────────────────────────────┘
                           │ Continue
                           v
┌─────────────────────────────────────────────────────────────┐
│                SEED CONFIRMATION                            │
│                   (Phase 1 - CRITICAL!)                     │
│  ┌───────────────────────────────────────────────────────┐ │
│  │   Confirm secret phrase                               │ │
│  │   Please tap on the correct answer...                 │ │
│  │                                                       │ │
│  │   Word #1                                             │ │
│  │   ┌──────┐  ┌──────┐  ┌──────┐                       │ │
│  │   │aware │  │wrong │  │bad   │                       │ │
│  │   └──✓───┘  └──────┘  └──────┘                       │ │
│  │                                                       │ │
│  │   Word #7                                             │ │
│  │   ┌──────┐  ┌──────┐  ┌──────┐                       │ │
│  │   │wrong │  │noise │  │bad   │                       │ │
│  │   └──────┘  └──✓───┘  └──────┘                       │ │
│  │                                                       │ │
│  │   Word #9                                             │ │
│  │   Word #12                                            │ │
│  │   (similar...)                                        │ │
│  │                                                       │ │
│  │   [Continue] ← Enabled when all selected             │ │
│  │                                                       │ │
│  │   ⚠️  Incorrect: 3 attempts remaining                 │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
│  Analytics: seed_confirmation_started                      │
│           : seed_confirmation_success (or failed)          │
│  File: seed_confirmation_screen.dart                       │
│  Logic: 4 random words, 3 choices each, 3 attempts         │
│  Security: Screenshot protected, cannot skip               │
└──────────────────────────┬──────────────────────────────────┘
                           │ All correct
                           v
┌─────────────────────────────────────────────────────────────┐
│              [MARK SEED AS BACKED UP]                       │
│         KomodoDefiSdk.confirmSeedBackup(true)               │
│         Clear seed & password from memory                   │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           v
┌─────────────────────────────────────────────────────────────┐
│                BIOMETRIC SETUP                              │
│                   (Phase 2 - OPTIONAL)                      │
│  ┌───────────────────────────────────────────────────────┐ │
│  │   [Face ID Icon]                                      │ │
│  │                                                       │ │
│  │   Secure your wallet                                  │ │
│  │   Turn on Face ID to secure your wallet.             │ │
│  │                                                       │ │
│  │   ┌──────────────────────────────────────┐            │ │
│  │   │  Enable Face ID                      │            │ │
│  │   └──────────────────────────────────────┘            │ │
│  │                                                       │ │
│  │   Skip for now                                        │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
│  Analytics: biometric_enabled OR biometric_skipped         │
│  File: biometric_setup_screen.dart                         │
│  Service: BiometricService.setEnabled(true/false)          │
└──────────────────────────┬──────────────────────────────────┘
                           │ Enable/Skip
                           v
┌─────────────────────────────────────────────────────────────┐
│                   WALLET READY                              │
│                   (Phase 2 - NEW!)                          │
│  ┌───────────────────────────────────────────────────────┐ │
│  │   [Success Illustration/Checkmark]                    │ │
│  │                                                       │ │
│  │   🎉 Brilliant, your wallet is ready!                 │ │
│  │                                                       │ │
│  │   Buy or deposit to get started.                      │ │
│  │                                                       │ │
│  │   ┌──────────────────────────────────────┐            │ │
│  │   │  Buy Crypto                          │            │ │
│  │   └──────────────────────────────────────┘            │ │
│  │                                                       │ │
│  │   I'll do this later                                  │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
│  Analytics: wallet_ready_shown                             │
│  File: wallet_ready_screen.dart                            │
└──────────────────────────┬──────────────────────────────────┘
                           │ Continue
                           v
┌─────────────────────────────────────────────────────────────┐
│                   [LOGIN TO WALLET]                         │
│              AuthBloc completes authentication              │
│              CoinsBloc starts session                       │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           v
┌─────────────────────────────────────────────────────────────┐
│                  MAIN WALLET VIEW                           │
│                   ✅ COMPLETE!                              │
│  ┌───────────────────────────────────────────────────────┐ │
│  │   [Wallet Dashboard]                                  │ │
│  │   • Portfolio overview                                │ │
│  │   • Asset list                                        │ │
│  │   • Transaction history                               │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
│  Analytics: onboarding_completed                           │
│  hasBackup: true ✅                                         │
└─────────────────────────────────────────────────────────────┘
```

---

## Existing User Flow (With Backup Warning)

```
┌─────────────────────────────────────────────────────────────┐
│                   APP LAUNCH (Returning)                    │
│              [Existing wallets detected]                    │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           v
┌─────────────────────────────────────────────────────────────┐
│                     WALLET LIST                             │
│                  (Skip start screen)                        │
│  ┌───────────────────────────────────────────────────────┐ │
│  │   My Wallets:                                         │ │
│  │   • Main Wallet (HD)                                  │ │
│  │   • Trading Wallet (Iguana)                           │ │
│  │   • Cold Storage (HD)                                 │ │
│  └───────────────────────────────────────────────────────┘ │
└──────────────────────────┬──────────────────────────────────┘
                           │ Select wallet
                           v
┌─────────────────────────────────────────────────────────────┐
│                    LOGIN SCREEN                             │
│  ┌───────────────────────────────────────────────────────┐ │
│  │   Enter password:                                     │ │
│  │   [________________]                                  │ │
│  │                                                       │ │
│  │   □ Remember me                                       │ │
│  │                                                       │ │
│  │   [Login]                                             │ │
│  └───────────────────────────────────────────────────────┘ │
└──────────────────────────┬──────────────────────────────────┘
                           │ Authenticate
                           v
┌─────────────────────────────────────────────────────────────┐
│              [CHECK HASBACKUP FLAG]                         │
│         If !hasBackup: Show banner                          │
└──────────────────────────┬──────────────────────────────────┘
                           │
                           v
┌─────────────────────────────────────────────────────────────┐
│                  MAIN WALLET VIEW                           │
│                  (with backup banner)                       │
│  ┌───────────────────────────────────────────────────────┐ │
│  │ ┌─────────────────────────────────────────────────┐   │ │
│  │ │ ⚠️  Komodo wallet requires you to backup your   │   │ │
│  │ │     seed phrase!                 [Backup] [✕]   │   │ │
│  │ └─────────────────────────────────────────────────┘   │ │
│  │                                                       │ │
│  │   [Normal wallet content]                             │ │
│  │   • Portfolio                                         │ │
│  │   • Assets                                            │ │
│  │   • Transactions                                      │ │
│  └───────────────────────────────────────────────────────┘ │
│                                                             │
│  Analytics: backup_banner_shown                            │
│  File: backup_warning_banner.dart                          │
│  Display: wallet_main.dart                                 │
└──────────────────────────┬──────────────────────────────────┘
                           │ Click "Backup"
                           v
┌─────────────────────────────────────────────────────────────┐
│              NAVIGATE TO SETTINGS > SECURITY                │
│              User can backup seed in settings               │
│                                                             │
│  Analytics: backup_banner_action_clicked                   │
└─────────────────────────────────────────────────────────────┘
```

---

## State Machine Diagram

```
┌────────────────────────────────────────────────────────────────┐
│                  WALLET CREATION FLOW                          │
│                                                                │
│  WalletCreationStep enum controls the state:                  │
│                                                                │
│  ┌─────────────┐                                              │
│  │   initial   │ ← Starting state                             │
│  └──────┬──────┘                                              │
│         │                                                      │
│         ├─────→ [User submits wallet form]                    │
│         │                                                      │
│         ↓                                                      │
│  ┌─────────────────┐                                          │
│  │ createPasscode  │ ← Phase 2 (optional)                     │
│  └──────┬──────────┘                                          │
│         │                                                      │
│         ↓                                                      │
│  ┌─────────────────┐                                          │
│  │confirmPasscode  │                                          │
│  └──────┬──────────┘                                          │
│         │                                                      │
│         ↓                                                      │
│  ┌─────────────┐                                              │
│  │   initial   │ ← Back to form                               │
│  └──────┬──────┘                                              │
│         │                                                      │
│         ├─────→ [AuthBloc creates wallet]                     │
│         │                                                      │
│         ↓                                                      │
│  ┌────────────────────┐                                       │
│  │ seedBackupWarning  │ ← Phase 1 (mandatory)                 │
│  └──────┬─────────────┘                                       │
│         │                                                      │
│         ↓                                                      │
│  ┌───────────────┐                                            │
│  │ seedDisplay   │                                            │
│  └──────┬────────┘                                            │
│         │                                                      │
│         ↓                                                      │
│  ┌──────────────────┐                                         │
│  │seedConfirmation  │ ← Quiz with 3 attempts                  │
│  └──────┬───────────┘                                         │
│         │                                                      │
│         ├─────→ [Mark hasBackup = true]                       │
│         │                                                      │
│         ↓                                                      │
│  ┌─────────────────┐                                          │
│  │ biometricSetup  │ ← Phase 2 (optional)                     │
│  └──────┬──────────┘                                          │
│         │                                                      │
│         ↓                                                      │
│  ┌─────────────────┐                                          │
│  │  walletReady    │ ← Success screen                         │
│  └──────┬──────────┘                                          │
│         │                                                      │
│         ↓                                                      │
│  ┌─────────────┐                                              │
│  │  complete   │ ← Trigger login                              │
│  └──────┬──────┘                                              │
│         │                                                      │
│         ↓                                                      │
│    [WALLET VIEW]                                              │
│                                                                │
└────────────────────────────────────────────────────────────────┘
```

---

## Analytics Event Flow

```
Start Screen Shown
    ↓
Onboarding Started (method: 'create')
    ↓
Passcode Created
    ↓
Onboarding Step Completed (step: 'passcode')
    ↓
Wallet Created (via existing event)
    ↓
Seed Backup Warning Shown
    ↓
Seed Displayed
    ↓
Seed Confirmation Started
    ↓
[If wrong] Seed Confirmation Failed (attempts: N)
[If correct] Seed Confirmation Success
    ↓
Biometric Enabled OR Biometric Skipped
    ↓
Wallet Ready Shown
    ↓
Onboarding Completed (method: 'create', duration: Nms)

─────────────────────────────────────

For existing users without backup:
    ↓
Backup Banner Shown
    ↓
[If clicked] Backup Banner Action Clicked
[If dismissed] Backup Banner Dismissed
```

---

## File Dependency Graph

```
main.dart
  ↓
app_bloc_root.dart
  ├─→ AuthBloc
  ├─→ AnalyticsBloc
  └─→ WalletsRepository
      ↓
main_layout.dart
  ↓
wallets_manager_wrapper.dart
  ├─→ OnboardingService (first launch check)
  ├─→ StartScreen (if first launch)
  └─→ WalletsManager
      ↓
iguana_wallets_manager.dart
  ├─→ WalletCreation (form)
  ├─→ PasscodeEntryScreen
  ├─→ PasscodeConfirmScreen
  ├─→ SeedBackupWarningScreen
  ├─→ SeedDisplayScreen
  ├─→ SeedConfirmationScreen
  ├─→ BiometricSetupScreen
  ├─→ WalletReadyScreen
  ├─→ PasscodeService
  ├─→ BiometricService
  └─→ KomodoDefiSdk (seed backup)

wallet_main.dart
  └─→ BackupWarningBanner
      └─→ Navigate to Settings
```

---

## Security Data Flow

```
Wallet Creation
    ↓
Password entered
    ↓
[Stored temporarily in _pendingWalletPassword]
    ↓
Wallet created via AuthBloc
    ↓
Retrieve seed: getMnemonicPlainText(password)
    ↓
[Seed stored temporarily in _pendingSeedPhrase]
    ↓
Seed displayed with ScreenshotSensitive wrapper
    ↓
User confirms seed
    ↓
confirmSeedBackup(hasBackup: true)
    ↓
[Clear _pendingSeedPhrase = null]
[Clear _pendingWalletPassword = null]
    ↓
✅ Sensitive data cleared from memory
```

---

## Color Coding Legend

- 🎨 **NEW Feature** (Phase 1 or 2)
- 📥 **Existing Feature** (Enhanced)
- ✅ **Complete** (Ready to use)
- ⏳ **Pending** (Future work)
- ⚠️ **Critical** (Security related)
- 🔒 **Mandatory** (Cannot skip)
- 🎯 **Optional** (Can skip)

---

**Document Version**: 1.0  
**Created**: October 2, 2025  
**Purpose**: Visual reference for complete authentication flow  
**Audience**: Developers, QA, Product Team

---

_Use this diagram when testing, explaining, or debugging the new authentication flow._
