ARG FRAPPE_BRANCH=develop
FROM node:14-buster
ARG FRAPPE_BRANCH=develop

ARG GITHUB_OWNER=msf4-0 			# you could give a default value as well
ENV GITHUB_OWNER=$GITHUB_OWNER

COPY install_frappe.sh /install_frappe
COPY install_erpnext.sh /install_erpnext
COPY install_app.sh /install_app
COPY prepare_production.sh /prepare_production

# Install frappe
RUN /install_frappe ${FRAPPE_BRANCH} && \
  # Install erpnext
  /install_erpnext && \
  # Install required apps with following command
  # /install_app <app_name> <repo> <app_branch>
  /install_app metabase_integration https://github.com/${GITHUB_OWNER}/ERPNext-Metabase-Integration master && \
  /install_app sql_accounting_software https://github.com/${GITHUB_OWNER}/ERPNext-SQL-Accounting-Integration main && \
  /install_app erpnext_telegram_integration https://github.com/${GITHUB_OWNER}/ERPNext-Telegram-Integration master && \
  /install_app frepple https://github.com/${GITHUB_OWNER}/ERPNext-Frepple-Enhanced-Integration main && \
  /install_app barcode_shrdc https://github.com/${GITHUB_OWNER}/ERPNext-Barcode-Integration master && \
  /install_app autocount https://github.com/${GITHUB_OWNER}/ERPNext-Autocount-Integration master && \
  /prepare_production

FROM frappe/erpnext-nginx:${FRAPPE_BRANCH}

COPY --from=0 /home/frappe/frappe-bench/sites/ /var/www/html/
COPY --from=0 /rsync /rsync

# Append list of installed to apps.txt
RUN echo -n "metabase_integration\nerpnext_telegram_integration\nbarcode_shrdc\nfrepple\nautocount\nsql_accounting_software" >> /var/www/html/apps.txt

VOLUME [ "/assets" ]

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["nginx", "-g", "daemon off;"]
