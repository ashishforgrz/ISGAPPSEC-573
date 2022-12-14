# ISGAPPSEC-573
For using UPDATE command in mysql -
function revokeAccessToken(token, client, user) {
    return OAuthAccessToken.findOne({
      where: {
        client_id: client.id,
        user_id: user.id
      },
    })
      .then(function () {
        var sql = "UPDATE oauth_access_tokens SET expires=? WHERE client_id=?, user_id=?";
        const expiredToken = token;
        expiredToken.accessTokenExpiresAt = new Date();
        OAuthAccessToken.query(sql,[expiredToken.accessTokenExpiresAt, client.id, user.id ], function (err, result){
          if (err) throw err;
        })
      })
      .catch(function (err) {
        logger.error('revokeToken1 - Err: ', err);
      });
}


Inbuilt in SQL scripts - 
function revokeAccessToken(token, client, user) {
    return OAuthAccessToken.findOne({
      where: {
        client_id: client.id,
        user_id: user.id
      },
    })
      .then(function () {
        const expiredToken = token;
        expiredToken.accessTokenExpiresAt = new Date();
        var sql = `UPDATE oauth_access_tokens SET expires=${expiredToken.accessTokenExpiresAt} WHERE client_id=${client.id}, user_id=${user.id}`;
        OAuthAccessToken.query(sql, function (err, result){
          if (err) throw err;
        })
      })
      .catch(function (err) {
        logger.error('revokeToken1 - Err: ', err);
      });
}
