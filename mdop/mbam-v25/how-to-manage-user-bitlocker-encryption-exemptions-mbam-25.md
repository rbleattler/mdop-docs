---
title: How to manage user BitLocker encryption exemptions
description: Microsoft BitLocker Administration and Monitoring (MBAM) allows you to exempt users from BitLocker Drive Encryption requirements.
author: aczechowski
ms.author: aaroncz
ms.collection: must-keep
ms.date: 06/16/2016
---

# How to manage user BitLocker encryption exemptions

Microsoft BitLocker Administration and Monitoring (MBAM) allows you to exempt users from BitLocker Drive Encryption requirements.

To exempt users from BitLocker protection, you have to:

- **Create an infrastructure to support exempted users.** Examples of this infrastructure include providing users with a contact telephone number, webpage, or mailing address that they can use to request an exemption.

- **Add the exempted user to a security group for a group policy object that is configured specifically for exempted users.** When members of this security group sign in to a computer, the user's group policy setting exempts the user from BitLocker protection. The user's group policy setting overwrites the computer policy, and the computer remains exempt from BitLocker encryption.

  > [!NOTE]
  > If the computer is already BitLocker-protected and the user is exempted, MBAM doesn't apply the encryption policy. However, if another user who isn't exempt from the encryption policy signs in to the computer, encryption starts.

The following steps describe what occurs when end users request an exemption from the BitLocker Drive Encryption exemption process through the MBAM client or through whatever process your organization uses. You must configure MBAM group policy settings to allow end users to request an exemption from BitLocker Drive Encryption.

1.  When end users sign in to a computer that is required to be encrypted, they receive a notification that their computer is going to be encrypted. They can select **Request Exemption** and postpone the encryption by selecting **Postpone**, or they can select **Start Encryption** to accept the BitLocker encryption.

    > [!NOTE]
    > Selecting **Request Exemption** postpones the BitLocker protection until the maximum time that's set in the User Exemption Policy.

2.  If end users select **Request Exemption**, they receive a notification telling them to contact the organization's BitLocker administration group. Depending on how the **Configure User Exemption Policy** is configured, users are provided with one or more of the following contact methods:

    - Phone number

    - Webpage URL

    - Mailing address

3.  After the exemption request is received, the MBAM administrator decides whether to add the user to the BitLocker Exemption Active Directory Domain Services (ADDS) group.

4.  After an end user submits an exemption request, the MBAM client reports the user as "Temporarily exempt." The Client then waits a specified number of days, which IT administrators configure, before it checks the computer's compliance again. If the MBAM administrator rejects the exemption request, the exemption request option is deactivated, which prevents the user from requesting the exemption again.

## To exempt a user from BitLocker Drive Encryption

1.  Create an ADDS security group to manage user exemptions from BitLocker encryption requirements.

2.  Create a group policy object by using the Microsoft BitLocker Administration and Monitoring group policy Templates.

3.  Associate the group policy object with the ADDS group that you created in the previous step. The policy settings to exempt users are located at: **UserConfiguration** &gt; **Administrative Templates** &gt; **Windows Components** &gt; **MDOP MBAM (BitLocker Management)**.

4.  To the security group you created for BitLocker exempted users, add the names of the users who are requesting an exemption.

    When a user signs in to a computer controlled by BitLocker, the MBAM client checks the User Exemption Policy setting. If the computer is already encrypted, BitLocker protection isn't suspended. If the computer isn't encrypted, MBAM doesn't prompt the user to encrypt.

    > [!NOTE]
    > Shared computer scenarios require special consideration when you use BitLocker user exemptions. If a non-exempt user signs in to a computer that's shared with an exempt user, the computer might be encrypted.

## Related articles

[Administering MBAM 2.5 features](administering-mbam-25-features.md)

[Planning for MBAM 2.5 group policy requirements](planning-for-mbam-25-group-policy-requirements.md)
