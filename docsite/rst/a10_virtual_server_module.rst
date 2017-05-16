.. _a10_virtual_server:


a10_virtual_server - Manage A10 Networks devices' virtual servers
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. versionadded:: 1.8


.. contents::
   :local:
   :depth: 1


Synopsis
--------

Manage slb virtual server objects on A10 Networks devices via aXAPI




Options
-------

.. raw:: html

    <table border=1 cellpadding=4>
    <tr>
    <th class="head">parameter</th>
    <th class="head">required</th>
    <th class="head">default</th>
    <th class="head">choices</th>
    <th class="head">comments</th>
    </tr>
            <tr>
    <td>host<br/><div style="font-size: small;"></div></td>
    <td>yes</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>hostname or ip of your A10 Networks device</div></td></tr>
            <tr>
    <td>password<br/><div style="font-size: small;"></div></td>
    <td>yes</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>admin password of your A10 Networks device</div></br>
        <div style="font-size: small;">aliases: pass, pwd<div></td></tr>
            <tr>
    <td>username<br/><div style="font-size: small;"></div></td>
    <td>yes</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>admin account of your A10 Networks device</div></br>
        <div style="font-size: small;">aliases: user, admin<div></td></tr>
            <tr>
    <td>validate_certs<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td>yes</td>
        <td><ul><li>yes</li><li>no</li></ul></td>
        <td><div>If <code>no</code>, SSL certificates will not be validated. This should only be used on personally controlled devices using self-signed certificates.</div></td></tr>
            <tr>
    <td>virtual_server<br/><div style="font-size: small;"></div></td>
    <td>yes</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>slb virtual server name</div></br>
        <div style="font-size: small;">aliases: vip, virtual<div></td></tr>
            <tr>
    <td>virtual_server_ip<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>slb virtual server ip address</div></br>
        <div style="font-size: small;">aliases: ip, address<div></td></tr>
            <tr>
    <td>virtual_server_ports<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>A list of ports to create for the virtual server. Each list item should be a dictionary which specifies the <code>port:</code> and <code>type:</code>, but can also optionally specify the <code>service_group:</code> as well as the <code>status:</code>. See the examples below for details. This parameter is required when <code>state</code> is <code>present</code>.</div></td></tr>
            <tr>
    <td>virtual_server_status<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td>enable</td>
        <td><ul><li>enabled</li><li>disabled</li></ul></td>
        <td><div>slb virtual server status</div></br>
        <div style="font-size: small;">aliases: status<div></td></tr>
            <tr>
    <td>write_config<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td>no</td>
        <td><ul><li>yes</li><li>no</li></ul></td>
        <td><div>If <code>yes</code>, any changes will cause a write of the running configuration to non-volatile memory. This will save <em>all</em> configuration changes, including those that may have been made manually or through other modules, so care should be taken when specifying <code>yes</code>.</div></td></tr>
        </table>
    </br>



Examples
--------

 ::

    # Create a new virtual server
    - a10_virtual_server: 
        host: a10.mydomain.com
        username: myadmin
        password: mypassword
        virtual_server: vserver1
        virtual_server_ip: 1.1.1.1
        virtual_server_ports:
          - port: 80
            protocol: TCP
            service_group: sg-80-tcp
          - port: 443
            protocol: HTTPS
            service_group: sg-443-https
          - port: 8080
            protocol: http
            status: disabled
    


Notes
-----

.. note:: Requires A10 Networks aXAPI 2.1


    
This is an Extras Module
------------------------

For more information on what this means please read :doc:`modules_extra`

    
For help in developing on modules, should you be so inclined, please read :doc:`community`, :doc:`developing_test_pr` and :doc:`developing_modules`.
