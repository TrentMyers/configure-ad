<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="stylesheet" href="styles.css">
</head>
<body>

<header>
  <i><b><h1>Configuring Active Directory in Azure</h1></b></i>
  <p>A comprehensive guide to setting up and managing Active Directory on Microsoft Azure, crafted meticulously for IT professionals and system administrators.</p>
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
  <p>Begin by establishing the foundational infrastructure within Microsoft Azure, including virtual machines and network configurations necessary for a robust Active Directory setup.</p>
  <h3>Create the Domain Controller VM</h3>
  <p>Name the VM <strong>DC-1</strong> with Windows Server 2022. Ensure that the VM is assigned a static Private IP address and document the associated Resource Group and Virtual Network details for future reference.</p>
  
  <h3>Create the Client VM</h3>
  <p>Similarly, establish a client VM named <strong>Client-1</strong> using Windows 10, aligning it within the same Resource Group and VNet to ensure seamless network communication. This setup is crucial for proper domain integration.</p>
  
</section>

<section id="ensure-connectivity">
  <h2>2. Ensure Connectivity</h2>
  <p>Validate network connectivity between your virtual machines to guarantee that the communication necessary for domain operations is in place.</p>
  <ol>
    <li>Using Remote Desktop, access Client-1 and execute <code>ping -t [DC-1 IP address]</code> to test continuous connectivity.</li>
    <li>Login to DC-1, and specifically allow ICMPv4 traffic through the local Windows Firewall settings.</li>

![image](https://github.com/TrentMyers/configure-ad/assets/132710625/1f5aad2e-35d6-4a39-ae4e-5c9b86783864)

    
    <li>Confirm successful communication via a continuous ping from Client-1 to DC-1.</li>
  </ol>
  
![image](https://github.com/TrentMyers/configure-ad/assets/132710625/8f02f181-b95f-47bb-8dd6-9c6337194a90)

  
</section>

<section id="install-ad">
  <h2>3. Install Active Directory</h2>
  <p>Proceed with installing and configuring Active Directory Domain Services to form the backbone of your network’s identity management.</p>
  <ol>
    <li>On DC-1, install Active Directory Domain Services (AD DS) role.</li>
    <li>Transform the server into a domain controller by initiating a new forest called <strong>mydomain.com</strong> and complete the domain setup.</li>
    <li>Upon completion, restart DC-1 and ensure you can log in with the domain administrator credentials <code>mydomain.com\labuser</code>.</li>
  </ol>
</section>

<section id="manage-users">
  <h2>4. Manage Users and Groups</h2>
  <p>Establish a structured user management framework by creating organizational units and defining user roles within Active Directory.</p>
  <ol>
    <li>Create organizational units (OUs) named "_EMPLOYEES" and "_ADMINS" to categorize and manage user accounts and administrative accounts, respectively.</li>
    <li>In the "_ADMINS" OU, create an administrator account for <strong>Jane Doe</strong> and assign her to the "Domain Admins" group, setting a precedent for role-based access control within your environment.</li>
  </ol>
</section>

<section id="join-domain">
  <h2>5. Join Client VM to Domain</h2>
  <p>Integrate your client VM into the newly established domain environment to enable centralized management and authentication.</p>
  <ol>
    <li>Modify DNS settings in the Azure Portal for Client-1 to utilize DC-1's IP address, ensuring domain name resolution is handled effectively.</li>
    <li>Reboot Client-1, and proceed to join it to the <strong>mydomain.com</strong> domain, finalizing its inclusion in the network.</li>
  </ol>
</section>

<section id="remote-desktop">
  <h2>6. Setup Remote Desktop for Users</h2>
  <p>Configure remote access capabilities to allow authorized domain users to connect to Client-1, enhancing flexibility and remote work options.</p>
  <ol>
    <li>As <code>jane_admin</code>, access the system properties of Client-1 and enable Remote Desktop, specifying access permissions for "domain users."</li>
  </ol>
  <!-- Consider adding a screenshot of the Remote Desktop configuration panel -->
</section>

<section id="additional-users">
  <h2>7. Create Additional Users and Test Logins</h2>
  <p>Expand your domain by adding more users and validating their operational capabilities through direct login tests.</p>
  <ol>
    <li>Utilize a PowerShell script on DC-1 to efficiently create multiple user accounts. The script can be accessed <a href="https://github.com/TrentMyers/AD-BULK-USERS">here</a>.</li>
    <li>Test the login process for newly created users on Client-1 to confirm their proper configuration and operational status within the domain.</li>
  </ol>
</section>

</body>
</html>

