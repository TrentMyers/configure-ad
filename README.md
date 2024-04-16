<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="styles.css"> <!-- Assuming you have a CSS file for styles -->
</head>
<body>

<header>
  <h1><i><b>Configuring Active Directory in Azure</b></i></h1>
  <p>A step-by-step guide to setting up Active Directory in Microsoft Azure.</p>
</header>

<nav>
  <h2>Table of Contents</h2>
  <ol>
    <li><a href="#setup-resources">Setup Resources in Azure</a></li>
    <li><a href="#ensure-connectivity">Ensure Connectivity</a></li>
    <li><a href="#install-ad">Install Active Directory</a></li>
    <li><a href="#manage-users">Manage Users and Groups</a></li>
    <li><a href="#join-domain">Join Client VM to Domain</a></li>
    <li><a href="#remote-desktop">Setup Remote Desktop for Users</a></li>
    <li><a href="#additional-users">Create Additional Users and Test Logins</a></li>
  </ol>
</nav>

<section id="setup-resources">
  <h2>1. Setup Resources in Azure</h2>
  <h3>Create the Domain Controller VM</h3>
  <p>Name the VM <strong>DC-1</strong> with Windows Server 2022. Note the Resource Group and Virtual Network created during this process. Ensure the Domain Controller's NIC Private IP address is set to static.</p>
  
  <h3>Create the Client VM</h3>
  <p>Name the VM <strong>Client-1</strong> with Windows 10, using the same Resource Group and Vnet. Ensure both VMs are within the same Vnet.</p>
  
  <!-- Here you can insert a screenshot showing the Azure portal with the VMs configured -->
</section>

<section id="ensure-connectivity">
  <h2>2. Ensure Connectivity</h2>
  <ol>
    <li>Login to Client-1 with Remote Desktop and use <code>ping -t [DC-1 IP address]</code> to test connectivity.</li>
    <li>Login to DC-1 and enable ICMPv4 on the local Windows Firewall.</li>
    <li>Verify that the ping from Client-1 to DC-1 is successful.</li>
  </ol>
  
  <!-- Diagram or screenshot showing successful ping results could be useful here -->
</section>

<section id="install-ad">
  <h2>3. Install Active Directory</h2>
  <ol>
    <li>Login to DC-1 and install Active Directory Domain Services (AD DS).</li>
    <li>Promote the server to a domain controller by setting up a new forest named <strong>mydomain.com</strong>.</li>
    <li>Restart DC-1 and log in as <code>mydomain.com\labuser</code>.</li>
  </ol>
</section>

<section id="manage-users">
  <h2>4. Manage Users and Groups</h2>
  <p>Create organizational units and users within Active Directory Users and Computers (ADUC).</p>
  <ol>
    <li>Create an OU called "_EMPLOYEES".</li>
    <li>Create another OU named "_ADMINS".</li>
    <li>Create a user named <strong>Jane Doe</strong> with username <code>jane_admin</code> and add her to the "Domain Admins" group.</li>
    <li>Use <code>jane_admin</code> as your admin account moving forward.</li>
  </ol>
</section>

<section id="join-domain">
  <h2>5. Join Client VM to Domain</h2>
  <ol>
    <li>Adjust DNS settings in Azure Portal for Client-1 to point to DC-1's IP.</li>
    <li>Restart Client-1, log in as local admin, and join it to <strong>mydomain.com</strong>.</li>
    <li>Verify the addition of Client-1 in ADUC on DC-1.</li>
  </ol>
</section>

<section id="remote-desktop">
  <h2>6. Setup Remote Desktop for Users</h2>
  <p>Configure Remote Desktop settings on Client-1 to allow domain users to connect.</p>
  <ol>
    <li>Login as <code>jane_admin</code> and modify system properties to enable Remote Desktop for "domain users".</li>
  </ol>
  <!-- Example or screenshot of the Remote Desktop settings could be included -->
</section>

<section id="additional-users">
  <h2>7. Create Additional Users and Test Logins</h2>
  <ol>
    <li>Use PowerShell on DC-1 to run a script for generating multiple user accounts. Script available <a href="https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1">here</a>.</li>
    <li>Log into Client-1 with a newly created user account to verify setup.</li>
  </ol>
</section>

</body>
</html>

